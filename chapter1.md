---
title: Test
description: >-
  Test


---
## Random constants

```yaml
type: MultipleChoiceExercise

xp: 50

key: a7fa8846b9
```

Tests on small data are great, but problems are often found on large datasets. However, some functions behave in predictable ways, even on random, large, data.

For example, if you took the whole dataset and added a constant _a_, then the maximum of the dataset would be the original maximum plus _a_. If you think about how the _distribution_ of the data is changed, you can think about how the results of functions applied to the data will also change.

Think about the standard statistical functions `min`, `max`, `median`, `mean`, `var` and `std`. Which of the following statements is true?

There is a small dataset in the `numpy` array `data` available in the shell.

`@instructions`
1. Any function `fn` applied to `data + a` will give the same result as `fn(data) + a`.
2. Any function `fn` applied to `data * a` will give the same result as `fn(data) * a`.
3. If the constant `a` makes `mean(data + a)` equal to zero, then `median(data + a)` also equals zero.
4. The variance and standard deviation of `data + a` are the same as `data`.

`@hint`
- Check what happens when you apply each function to `data` in the terminal, trying values for `a` such as `2` or `0.1`.
- Try computing `mean(data - mean(data))` to find interesting values of `a`.
- How does the _shape_ of the distribution affect things?

`@pre_exercise_code`
```{python}
import numpy as np
np.random.seed(42)

data = np.random.rand(100)
```






