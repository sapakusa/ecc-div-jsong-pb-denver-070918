
# Finite Field Division

The intuition that helps us with addition, subtraction, multiplication and perhaps even exponentiation unfortunately doesn’t help us quite as much in division. Generally speaking division is the hardest one to make sense of, but we’ll start with something that should make sense.

In normal math, division is the opposite of multiplication:

7⋅8 = 56 implies that 56/8 = 7

12⋅2 = 24 implies that 24/12 = 2

And so on. We can use this as the definition of division to help us. Note that like normal math, you cannot divide by 0.

In \\(F_{19}\\, we know that:

3⋅7=21%19=2 implies that 2/7=3

9⋅5=45%19=7 implies that 7/5=9

This is very unintuitive as we generally think of 2/7 or 7/5 as fractions, not nice round field elements. Yet that is one of the remarkable things about Finite Fields: Finite Fields are closed under division. That is, dividing any two numbers where the denominator is not 0 will result in another field element.

The question you might be asking yourself is, how do I calculate 2/7 if I didn’t know 3⋅7=2? This is indeed a very good question and in order to answer it, we’ll have to use the result from the previous exercise.

You probably noticed that n(p-1) is always 1. This is a beautiful result from number theory called Fermat’s Little Theorem and only works when p is prime. Essentially, the theorem says:

n(p-1)%p=1 where p is prime

Since we are operating in prime fields, this will always be true.

### Try it

#### Solve these equations in \\(F_{31}\\):

\\(3/24 = ?\\)

\\(17^{-3} = ?\\)

\\(4^{-4}\cdot{11} = ?\\)



```python
# remember pow(x, p-2, p) is the same as 1/x in F_p
prime = 31
# 3/24 = ?
print(3*24**(prime-2) % prime)
# 17^(-3) = ?
print(pow(17, prime-4, prime))
# 4^(-4)*11 = ?
print(pow(4, prime-5, prime) * 11 % prime)
```

### Test Driven Exercise

Create the `__truediv__` method for your library:


```python
from ecc import FieldElement

class FieldElement(FieldElement):

    def __pow__(self, n):
        # remember fermat's little theorem:
        # self.num**(p-1) % p == 1
        # you might want to use % operator on n
        prime = self.prime
        num = pow(self.num, n % (prime-1), prime)
        return self.__class__(num, prime)

    def __truediv__(self, other):
        if self.prime != other.prime:
            raise RuntimeError('Primes must be the same')
        # self.num and other.num are the actual values
        num = (self.num * pow(other.num, self.prime - 2, self.prime)) % self.prime
        # self.prime is what you'll need to mod against
        prime = self.prime
        # use fermat's little theorem:
        # self.num**(p-1) % p == 1
        # this means:
        # 1/n == pow(n, p-2, p)
        # You need to return an element of the same class
        # use: self.__class__(num, prime)
        return self.__class__(num, prime)
```
