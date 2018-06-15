# Finite Field Division

#### 3.1. Solve these equations in \\(F_{31}\\):

\\(3/24 = ?\\)

\\(17^{-3} = ?\\)

\\(4^{-4}\cdot{11} = ?\\)

#### 3.2. Write a program to calculate \\(k/1, k/2, k/3, ...k/30\\) for some k in \\(F_{31}\\). Notice anything about these sets?

#### 3.3. Make [these tests](/edit/session1/ecc.py) pass:

```
ecc.py:FieldElementTest:test_div
```


```python
# Exercise 3.1

# remember pow(x, p-2, p) is the same as 1/x in F_p
prime = 31
# 3/24 = ?
# 17^(-3) = ?
# 4^(-4)*11 = ?
```


```python
# Exercise 3.2

from random import randint

prime = 31
k = randint(1, prime)

# use range(31) to iterate over all numbers from 0 to 30 inclusive
```


```python
# Exercise 3.3

reload(ecc)
run_test(ecc.FieldElementTest('test_div'))

# Hint: the __pow__ method needs a positive number for the exponent.
# You can mod by p-1
```
