# Prompt: Quantify Factors (Tier A statistical validation)

Use this when `explain.md` Step 4.3 determines Tier A data (n > ~30, cross-sectional or panel) is available. This turns "I think X matters more than Y" into a checkable number.

## Concepts (plain-language paired, per report.md's annotation rule)

**Standardized beta (β)** (the independent influence of a factor after removing the effect of every other factor — the bigger the number, the more it matters on its own): standardize every variable (subtract mean, divide by standard deviation) then run a multivariate regression. β = -0.36 means a 1-standard-deviation increase in this factor is associated with a 0.36-standard-deviation decrease in the outcome, *holding the other factors constant*.

**Single-variable correlation (r)** (how strongly this factor moves together with the outcome on its own — can be misleading, since it doesn't control for anything else): Pearson r (linear) and Spearman ρ (monotonic, catches non-linearity) computed independently for each candidate factor against the outcome.

**Compression rate** (how much of a factor's apparent relationship is actually "borrowed" from another factor — the higher this number, the less independent the factor really is):
```
compression = (|r| - |β|) / |r| x 100%

< 40%   -> essential factor candidate (mostly independent contribution)
40-70%  -> mediating factor candidate (partly relayed through another variable)
> 70%   -> proxy/confounding variable (most of the effect vanishes once controlled)
```

**VIF — variance inflation factor** (how much two candidate factors are "tangled together" — if they're too tangled you can't tell which one deserves credit): VIF > 10 between a pair of factors signals collinearity; keep the more theoretically fundamental one (usually the one further down its 5Why chain) and drop or merge the other.

**Granger-style lead-lag** (checks whether X's past values help predict Y's future beyond what Y's own past already tells you — this is a "leading indicator" test, not proof of true causation): use for time-series factors when a full regression isn't appropriate.

## Workflow

1. Compute single-variable `r` (Pearson + Spearman) for every candidate factor against the outcome. Rank.
2. Put all candidate factors into one multivariate regression, get standardized `β` for each.
3. Compute `compression` per factor from steps 1-2. Classify per `explain.md` Step 4.4's role table.
4. Check VIF between highly-correlated factor pairs; resolve collinearity.
5. Where relevant, run the cross-group / robustness check from `explain.md` Step 4.5 — recompute β within each sub-group and see how much it moves.

## Reusable Python snippet

```python
import pandas as pd
from scipy import stats
import statsmodels.api as sm
from sklearn.preprocessing import StandardScaler

def layered_correlation(df, y_col, factor_cols):
    """Step 1: single-variable r / rho per factor."""
    results = []
    for col in factor_cols:
        mask = df[[col, y_col]].dropna().index
        r, p = stats.pearsonr(df.loc[mask, col], df.loc[mask, y_col])
        rho, p_s = stats.spearmanr(df.loc[mask, col], df.loc[mask, y_col])
        results.append({'factor': col, 'pearson_r': round(r, 3),
                         'p_pearson': round(p, 4), 'spearman_rho': round(rho, 3)})
    return pd.DataFrame(results).sort_values('pearson_r', key=abs, ascending=False)

def standardized_beta(df, y_col, factor_cols):
    """Step 2-3: standardized beta + compression rate + role classification."""
    scaler = StandardScaler()
    data = df[[y_col] + factor_cols].dropna()
    scaled = pd.DataFrame(scaler.fit_transform(data), columns=data.columns)
    X = sm.add_constant(scaled[factor_cols])
    model = sm.OLS(scaled[y_col], X).fit()
    betas = model.params.drop('const')
    pvals = model.pvalues.drop('const')
    r_vals = {col: stats.pearsonr(data[col], data[y_col])[0] for col in factor_cols}
    result = pd.DataFrame({
        'beta': betas.round(3),
        'p_value': pvals.round(4),
        'r': pd.Series(r_vals).round(3),
    })
    result['compression'] = ((result['r'].abs() - result['beta'].abs())
                              / result['r'].abs() * 100).round(1)
    result['role'] = result['compression'].apply(
        lambda x: 'essential' if x < 40 else ('mediating' if x < 70 else 'confounding'))
    return result.sort_values('beta', key=abs, ascending=False)

def cross_group_stability(df, y_col, factor_cols, group_col):
    """Step 5: robustness — how much does beta move across sub-groups?"""
    out = {}
    for g, sub in df.groupby(group_col):
        try:
            out[g] = standardized_beta(sub, y_col, factor_cols)['beta']
        except Exception:
            continue
    return pd.DataFrame(out)
```

## Discipline

- Always report `r` **and** `β` side by side — reporting only one is incomplete (a high `r` with a high compression rate is the single most common way an analysis fools itself).
- p-values, R², and VIF thresholds are guides, not magic numbers — state them, but don't treat "p = 0.049 significant, p = 0.051 not" as a meaningful distinction.
- If sample size is too small for Tier A (`n` below roughly 30, or too few observations per candidate factor relative to the number of factors), say so and drop to Tier B/C/D per `explain.md` Step 4.3 rather than running an underpowered regression and presenting it with false confidence.
