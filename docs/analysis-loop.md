# The Analysis Loop

```
        +-----------------------------------------------------+
        |                                                       |
        v                                                       |
    [Define] --> [Model] --> [Observe] --> [Explain] --> [Predict] --> [Optimize]
                                  ^                         |
                                  |                         |
                                  +----- new evidence -------+
                                     (if prediction is tested
                                      and diverges from reality)
```

The loop is not strictly linear in practice: predictions that fail against reality feed back into Observe as new evidence, refining the model and hypotheses. Analysis OS treats this as expected — a "final" analysis is really just the current best state of an ongoing loop, and reports should be versioned/dated rather than treated as permanent truth.
