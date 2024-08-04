# From arithmetics to boolean algebra

So the goal with this is more to see if it's possible to define math operations with **Arithmetic operations**, **Algebra rules**, **Series and Sequences**. 

> I could not find any information about this subject, anywhere. 
> So much of this "seems" to not have been explored in this nature. There is obviously boolean algebra, but it's formalised with different axioms.


### Quick notes
Most of these operations and functions work because of infinite series.
So to make this computable we should define a maximum number length so that we know how to specify the series so that they correctly converges. 

For periodic functions we also would use range reduction. 

*The base formulas are defined at the bottom*.

#### Irreducibility
When starting to formalise these expressions you sometimes discover cases where some expressions cannot be simplified (reduced) anymore, because then they'd lose their unique property. So those expressions often get their own math notation.

#### Regular functions
Let me give you an example. Take the Modulo function. Its definition includes the Absolute- and the Floor function. But how are they defined?

The Absolute function is very simple, we've seen it many times in action. It has this signature, $\sqrt{x^2}$.

Let us define it as: 

$$|x|=\sqrt{x^2}$$

> Note that if we have a complex number $|z|$ would be interpreted as $\sqrt{a^2 + b^2}$. But here we say it's $\sqrt{x^2}$, which then would mean that $\sqrt{(-(real + imaginary))^2} = real + imaginary$.

The *mod/floor/ceil/fraction* functions are always based on eachother, which makes it a little frustrating to define it using our method. But after playing around with trigonometric functions, I've managed to find out that we only need to define the *modulo* operation, and the rest can be derived from it. Took me a while to figure this out..

Lets define it as: 

$$mod(x, y) = \frac{y\times\cot^{-1}(\cot(\frac{\pi x}{y}))}{\pi}$$
>This function can not be found anywhere on the internet and is very important in our case, because it's the building block for many of the following functions.

Let us define: 

$$ \{x\} = frac(x) = mod(x, 1)$$

> This will give us the faction part.

We can also define $trunc(x)$:

$$trunc(x) = x - sign(x) \cdot mod(|x|, 1)$$
> $sign(x)$ is defined in the logical expressions section.

So with this, we can define the $\lfloor x \rfloor$ function.

Lets define it as: 

$$\lfloor x \rfloor = floor(x) = x - \{x\}$$

We can also define the $\lceil x \rceil$ function now.

Lets define it as: 

$$\lceil x \rceil = ceil(x) = x +  \{-x\}$$

We can also define $round(x)$, both up and down.

Let us define it as: 

$$roundUp(x) = \lfloor x + 0.5 \rfloor$$

Let us define it as: 

$$roundDown(x) = \lceil x - 0.5 \rceil$$

We can also define the $isFraction(x)$ function.

Lets define it as:

$$isFraction(x) = \lceil x \rceil - \lfloor x \rfloor$$

We define the $length(x)$ function, which gives us the integer length of a number.

Lets define it as: 

$$length(x) = \lfloor \log_{10}(|x|) \rfloor + 1$$
> Note that we need to specify a MAX fraction size if we want to be able to count the number length of fractions/decimals.

We can define the $digitAt(x, pos) = number_{position}$, which gives us the integer number at position.

Lets define it as: 

$$digitAt(x, pos) = \lfloor \frac{\lfloor x - \lfloor \frac{x}{10^{pos}} \rfloor \cdot 10^{pos} \rfloor}{10^{pos - 1}} \rfloor$$

> Important, I've seen that $\lfloor \frac{x}{10^{pos - 1}} \rfloor \bmod 10$ doesn't give accurate digits when working with contiguous bit sequences, so I would use my version instead.



### Logical expressions

We can now move over to more logical operations. Lets start by talking about $0^{x}$. The power rule states that $0^{x > 0} = 0$, and $0^{x = 0} = 1$. It's important to note that $0^{0}$ is actually indeterminate, and has different defitions depending on the context. In combinatorics, it is defined as being equal to one, but using limits, one could argue for it being equal to either 1 or 0.

Now to really formalize this expression such that it's defined for all *x* (making it sound), we can actually define it as: 

$$\text{\textit{off}}\ (x) = 0^{|x|+x} = \begin{cases} 0 & \text{if } x > 0 \\
1 & \text{if } x \leq   0\end{cases}$$

$$0^{|x|}0^{x}=0^{x}0^{|x|}=0^{|x|\ +\ x} \ \ \text{Doesn't work}$$

$$(|x| - x)^{|x|}(|x| - x)^{x}=(|x| - x)^{x}(|x| - x)^{|x|}=(|x| - x)^{|x|\ +\ x}=0^{|x|\ +\ x} \ \ \text{Works}$$

>I also want to share this expression $(|x|\ -\ x)^{|x|\ +\ x}$, which has the same properties as $0^{|x|\ +\ x}$.

We can also define it as this:

$$ \text{\textit{off}}\ (-x) = 0.5 + \frac{|x - mod(x, 1) + 0.5|}{2x - 2 \times mod(x, 1) + 1}$$

>This would actually require $(|x|\ -\ x)^{|x|\ +\ x}$ because *mod* (arccot to be specific) uses piecewise notation.

Next up is $on(x)$, and it is basically just a negation.

$$on(x) = 1 - \text{\textit{off}}\ (x) = \begin{cases} 1 & \text{if } x > 0 \\
0 & \text{if } x \leq   0\end{cases}$$

>I've later discovered that these functions I'm defining here are often called **step function, heaviside function, boxcar function**, but they define it differently.
>They are often defined using piece-wise functions. The main difference here is that I'm saying that 0 is part of the negative number line.

We can also define the $sign(x)$ function. Its codomain looks like this:

$$sign(x) = (-1)^{on(-x)} = \begin{cases} +1 & \text{if } x \geq   0 \\
-1 & \text{if } x < 0 \end{cases}$$

So next up is to define the basic $not(x)$, $and(x, y)$, and $or(x, y)$.

Let us define: 

$$not(x) = 1 - on(x) = on(\text{\textit{off}}\ (x))$$

$$and(x, y) = on(x) \times on(y)$$

$$or(x, y) = not(and(not(x), not(y)))$$

$$xor(x, y) = or(and(not(x), y), and(x, not(y)))$$

The $max(a, b)$ function can easily be defined using the previous logic operations.

Let us define it as:

$$max(a, b) = a\cdot on\left(a\ -\ b\right)\ +\ b\cdot\left(1\ -\ on\left(a\ -\ b\right)\right)$$

and the $min(a, b)$ function can then just switch the arguments around.

$$min(a, b) = b\cdot on\left(a\ -\ b\right)\ +\ a\cdot\left(1\ -\ on\left(a\ -\ b\right)\right)$$

Let's do *Greater than*, *Lesser than* / *or equal*.

Greater than or equal:

$$x \geq a = gte(x, a) = 0^{\left|a\ -\ \min\left(x,\ a\right)\right|}$$

Lesser than or equal:

$$x \leq a = lte(x, a) = 0^{\left|a\ -\ \max\left(x,\ a\right)\right|}$$

Greater than:

$$x \gt a = gt(x, a) = 1-lte(x, a)$$

Lesser than:

$$x < a = lt(x, a) = 1-gte(x, a)$$

... we can go on and on...

Open interval:

$$between(x, a, b) = a < x < b = 0^{|on(x - a) - on(-x - b)|} = on(x - a) - 0^{|(x - b)| - (x-b)} =\begin{cases} 1 & \text{if } a \lt x \lt b \\ 
0 & \text{else }\end{cases}$$

Half-open interval:

$$ = \lbrack\ a,\ b\ \rparen (x) = gte(x, a) \times lt(x, a) \times x$$


We can do a binary counting function:

$$fromBinaryToDecimal(x)=\sum_{n=0}^{length(x)} on(digitAt(x, n + 1)) \cdot 2^{n}$$

$$fromBinaryToDecimal(1010101) = 85$$

We can do a binary16 (IEEE Standard for Floating-Point Arithmetic) to decimal:

$$ fromBinary16ToDecimal(x) = \left(-1\right)^{digitAt\left(x,\ 16\right)} \cdot 2^{(\sum_{n=0}^{4}digitAt\left(x,\ 11\ +\ n\right)\cdot2^{n})-15} \cdot \left(1\ +\ \sum_{n=0}^{9}digitAt\left(x,\ 10\ -\ n\right)\cdot2^{-\left(n\ +\ 1\right)}\right)$$

$$fromBinary16ToDecimal(0100001100000000) = 3.5$$

> This is just a proof of concept for turning a binary sequence number only containing 1 and 0 into a decimal number.


### Piecewise functions

But now we can do Piecewise functions with "pure" math.

$$f(x) = between(x, 0, 4) \times x^{2} + between(x, 3, 6) \times x^{3}$$

....

### Special Fourier series

Rectangular function can be defined using the logical operations above. But it's also possible to define it using a logistic function IIF we have defined $\frac{x}{0} = \infty$, and $\frac{x}{\infty} = 0$.

$$rect(x)= \frac{1}{1 + 0^{x + 0.5}} - \frac{1}{1 + 0^{x - 0.5}}$$

----------------------

### Base formulas 

> NOTE: There're certain Analytical continuations for certain functions, but that's not the point of this.

$$ln(x) = 2 \times \sum_{n=0}^{\infty} \frac{1}{2n + 1}(\frac{x - 1}{x + 1})^{2n+1}$$

$$e^{x} = \sum_{n=0}^{\infty} \frac{x^{n}}{n!}$$

$$b^{x} = e^{x \times ln(b)}$$

$$x! = \lim_{N \to \infty} N^x\prod^{N}_{k=1} \frac{k}{k + x}$$

$$sin(x) = \sum_{n=0}^{\infty} \frac{(-1)^{n}}{(2n + 1)!} x^{2n + 1} = \frac{x}{(\frac{x}{\pi})!(-\frac{x}{\pi})!}$$

$$cos(x) = \sum_{n=0}^{\infty} \frac{(-1)^{n}}{(2n)!} x^{2n} = sin(x + \frac{\pi}{2})$$

$$\pi cot(\pi x)= \lim_{N \to \infty} \sum_{n=-N}^{N} \frac{1}{x + n}$$

$$tan^{-1}(x)=\sum_{n = 0}^{\infty} \frac{(-1)^n}{2n + 1} x^{2n + 1} = \int_{0}^{n}\frac{1}{1\ +\ x^{2}}dx$$

$$
cot^{-1}(x) = \begin{cases} \frac{\pi}{2} - tan^{-1}(x) & \text{if } -1 \leq x \leq 1 \\
tan^{-1}(\frac\{1}{x}) & \text{if } x \geq 1 \\
\pi + tan^{-1}(\frac\{1}{x}) & \text{if } x \leq -1 \end{cases} = \frac{\pi}{2} - \int_{0}^{n}\frac{1}{1\ +\ x^{2}}dx 
$$

$$\int^{\infty}_{0} t^{x-1}e^{-t}dt$$

$$N^x\prod^{\infty}_{k=1} \frac{k}{k + x}$$

etc..


### notes

TODO: Expand these subject
1. Numerical stability
2. Trigonometry functions
3. Gamma function
4. Numerical Integration




