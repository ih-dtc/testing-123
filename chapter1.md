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
## Building a test

```yaml
type: TabExercise

xp: 100

key: c7668b0bd0
```

We want to build a test: a function that can _repeatably_ check if our code is correct. You will do this step-by-step.











***



```yaml
type: NormalExercise

xp: 25

key: 13c92cf98a
```



`@instructions`
Generate "random" data $x$ and fix a constant $c$ and check that the minimum of $x$ plus the constant $c$ is the minimum of $x + c$.

- Set the random seed to 42.
- Generate `x` containing 10,000 random numbers.
- Set `c` to be the constant 1.
- Compare $\min(x + c)$ to $\min(x) + c$, printing if they match.

`@hint`
Make sure to set the random seed to `42` first.


`@sample_code`
```{undefined}
# Import numpy

# Set the random seed to 42
np.random.seed(___)
# Generate x containing 10000 random numbers
x = np.random.rand(___)
# Set c to 1

# Compare min(x + c) to min(x) + c: result
result = ___ == ___
# Print the result
print(___)
```
`@solution`
```{undefined}
# Import numpy
import numpy as np
# Set the random seed to 42
np.random.seed(42)
# Generate x containing 10000 random numbers
x = np.random.rand(10000)
# Set c to 1
c = 1
# Compare min(x + c) to min(x) + c: result
result = min(x + c) == min(x) + c
# Print the result
print(result)
```
`@sct`
```{undefined}
Ex().test_object("x")
Ex().test_object("c")
Ex().test_object("result")
```






***



```yaml
type: NormalExercise

xp: 25

key: caa80368fa
```



`@instructions`
Using a fixed constant $c$ isn't a general test. Using a random single number would be better. But comparing floating point numbers added together is risky. Instead of using direct equality, use the `numpy` `allclose` function to see if the results are _close enough_.

- Set the random seed to 42.
- Generate `x` containing 10,000 random numbers.
- Generate `c` containing a single random number.
- Compare $\min(x + c)$ to $\min(x) + c$, printing if they are close enough.

`@hint`
`np.allclose` takes two inputs and compares if all elements are sufficiently close together.


`@sample_code`
```{undefined}
# Import numpy
import numpy as np
# Set the random seed to 42

# Generate x containing 10000 random numbers

# Generate c containing one random number

# Compare min(x + c) to min(x) + c: result
result = ___
# Print the result
print(result)
```
`@solution`
```{undefined}
# Import numpy
import numpy as np
# Set the random seed to 42
np.random.seed(42)
# Generate x containing 10000 random numbers
x = np.random.rand(10000)
# Generate c containing one random number
c = np.random.rand()
# Compare min(x + c) to min(x) + c: result
result = np.allclose(min(x + c), min(x) + c)
# Print the result
print(result)
```
`@sct`
```{undefined}
Ex().test_object("x")
Ex().test_object("c")
Ex().test_object("result")
```






***



```yaml
type: NormalExercise

xp: 25

key: c787333c6c
```



`@instructions`
Typing out a half-dozen lines of code every time we want to repeat the test is going to get very annoying, very fast.

Convert your code into a function, `test_min`. It should take no arguments and return the `result`, a boolean saying if the test passed.

`@hint`



`@sample_code`
```{undefined}
# A solution of the previous exercise
import numpy as np
# Convert the following code to a function
np.random.seed(42)
x = np.random.rand(10000)
c = np.random.rand()
result = np.allclose(min(x + c), min(x) + c)
# After coding the function, call it and print the result
print(result)
```
`@solution`
```{undefined}
# A solution of the previous exercise
import numpy as np
# Convert the following code to a function
def test_min():
  np.random.seed(42)
  x = np.random.rand(10000)
  c = np.random.rand()
  result = np.allclose(min(x + c), min(x) + c)
  return result
# After coding the function, call it and print the result
print(test_min())
```
`@sct`
```{undefined}
Ex().test_function("test_min")
```






***



```yaml
type: NormalExercise

xp: 25

key: 1780e19ab4
```



`@instructions`
Imagine you have built a test for all the statistical functions. Checking the output of every test for every function is going to be dull and error-prone.

Instead, our testing function should only care is the test _fails_. In this case things are sufficiently bad that it should appear as an error, or an _exception_.

Change your test from the previous solution so that, instead of returning a boolean result, it instead uses the `assert` function to check if the test passed.

`@hint`
`assert` takes a single boolean (`True` or `False`) statement and does nothing (if the statement is `True`) or raises an exception (if the statement is `False`).


`@sample_code`
```{undefined}
# A solution of the previous exercise
import numpy as np
# The testing function
def test_min():
  np.random.seed(42)
  x = np.random.rand(10000)
  c = np.random.rand()
  result = np.allclose(min(x + c), min(x) + c)
  return result
# After coding the function, call it to check the test passes
test_min()
```
`@solution`
```{undefined}
# A solution of the previous exercise
import numpy as np
# The testing function
def test_min():
  np.random.seed(42)
  x = np.random.rand(10000)
  c = np.random.rand()
  assert(np.allclose(min(x + c), min(x) + c))
# After coding the function, call it to check the test passes
test_min()
```
`@sct`
```{undefined}
Ex().has_equal_error()
```









---
## Building a test

```yaml
type: NormalExercise

xp: 100

key: 0bb22dda3d
```

You checked that shifting a distribution, by adding a constant to the data, does not change its variance. You now need to write a test that checks that this is true: it should generate some data $x$ and check that $\mathrm{var}(x)$ is the same as $\mathrm{var}(x + c)$ for constant $c$.

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
# Check that the passes or fails the same way as the model
exceptions = []
for my_var in (np.var, np.mean):
    try:
    	test_variance()
    except AssertionError as e:
    	exceptions.append(e)
    else:
    	exceptions.append(None)

Ex.test_object(exceptions)


# Check the import
Ex.test_import("numpy")

# Check the function
```





