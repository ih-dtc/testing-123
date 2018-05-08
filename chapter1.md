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


`@sct`
```{python}
msg1 = "Not quite: check the results for the variance and standard deviation."
msg2 = "No: what happens with the variance?"
msg3 = "This would only be true with symmetric data!"
msg4 = "Excellent! How would you turn this into a test?"
test_mc(4, [msg1, msg2, msg3, msg4])
```





---
## Insert exercise title here

```yaml
type: NormalExercise

xp: 100

key: 0bb22dda3d
```

You checked that shifting a distribution, by adding a constant to the data, does not change its variance. You now need to write a test that checks that this is true: it should generate some data $x$ and check that $\var(x)$ is the same as $\var(x + c)$ for constant $c$.

A function `my_var` that takes a numpy array `x` and computes its variance is available in your namespace.

`@instructions`
Write a unit test `test_variance()` that checks that `my_var` behaves correctly when a constant is added to the data.

- `test_variance` takes no arguments.
- the test should first set the random seed to `42`.
- the test should generate a random array `x` of size $10,000$.
- the test should compare `my_var(x)` to `my_var(x + c)`, where `c` is a random number.

`@hint`
The variance will be a floating point number. Use `assert` and the `allclose` function from `numpy` to compare the values.

`@pre_exercise_code`
```{python}
import numpy as np
my_var = np.var
```
`@sample_code`
```{python}
# Import numpy: we need to do floating point comparisons


# Define the unit test
def test_variance():
  # Create the "random" data
  
  
  
  # Assert that adding a constant does not change the variance
  
```
`@solution`
```{python}
# Import numpy: we need to do floating point comparisons
import numpy as np

# Define the unit test
def test_variance():
  # Create the "random" data
  np.random.seed(42)
  x = np.random.rand(10000)
  c = np.random.rand()
  # Assert that adding a constant does not change the variance
  assert(numpy.allclose(my_var(x), my_var(x + c)))
```
`@sct`
```{python}
import pytest

pytest.main()
```



