# Symbolic math

So the goal with this is more to see if it's possible to define certain math operations with just using **Arithmetic operations**, **Algebra rules**, **Series and Sequences**.


> I could not find any information about this subject, anywhere. 
> So much of this "seems" to not have been explored (or even cared about).


> NOTE: There're certain Analytical continuations for certain functions, but that's not the point of this.


$$ln(x) = 2 \times \sum_{n=0}^{\infty} \frac{1}{2n + 1}(\frac{x - 1}{x + 1})^{2n+1}$$

$$e^{x} = \sum_{n=0}^{\infty} \frac{x^{n}}{n!}$$

$$b^{x} = e^{x \times ln(b)}$$

$$x! = \lim_{N \to \infty} N^x\prod^{N}_{k=1} \frac{k}{k + x}$$

$$sin(x) = \sum_{n=0}^{\infty} \frac{(-1)^{n}}{2n + 1} x^{2n + 1}$$

$$cos(x) = \sum_{n=0}^{\infty} \frac{(-1)^{n}}{2n} x^{2n}$$

$$\pi cot(\pi x)= \lim_{N \to \infty} \sum_{n=-N}^{N} \frac{1}{x + n}$$

$$tan^{-1}(x)=\sum_{n = 0}^{\infty} \frac{(-1)^n}{2n + 1} x^{2n + 1}$$

$$
cot^{-1}(x) = \begin{cases} \frac{\pi}{2} - tan^{-1}(x) & \text{if } -1 \leq x \leq 1 \\
tan^{-1}(\frac\{1}{x}) & \text{if } x \geq 1 \\
\pi + tan^{-1}(\frac\{1}{x}) & \text{if } x \leq -1 \end{cases}
$$

> Trig functions here...

### Regular functions
Let me give you an example. Take the Modulo operator. Its definition includes the Absolute- and the Floor operator. But how are they defined?

The Absolute operator is very simple, we've seen it many times in action. It has this signature, $\sqrt{x^2}$.

Let us define it as: $$|x|=\sqrt{x^2}$$

Now, the Floor operator can actually be defined by the Modulo operator. It's a bit tricky, so to define it, we have to use two trigonometry functions. Took me a while to figure this out..

Lets define it as: $$mod(x, y) = \frac{y\times\cot^{-1}(\cot(\frac{\pi x}{y}))}{\pi}$$
>This function can not be found anywhere on the internet.

Let us define: $$truncate(x) = mod(x, 1)$$

So with this, we can define the $\lfloor x \rfloor$ operator.

Lets define it as: $$\lfloor x \rfloor = x - truncate(x)$$

We can also define the $\lceil x \rceil$ operator now.

Lets define it as: $$\lceil x \rceil = x + truncate(-x)$$

We can also define $round(x)$, both up and down.

Let us define it as: $$roundUp(x) = \lfloor x + 0.5 \rfloor$$

Let us define it as: $$roundDown(x) = \lceil x - 0.5 \rceil$$


### Logical expressions
We can now move over to more logical operators. We begin with $true(x)$. Its codomain looks like this.

$$true(x) = 1 - 0^{|x|+x} = \begin{cases} 1 & \text{if } x > 0 \\
0 & \text{if } x \leq   0\end{cases}$$

>I've later discovered that these functions I'm defining here are often called **step function, heaviside function, boxcar function**.
>They are often defined using piece-wise functions. The main difference here is that I'm saying that 0 is part of the negative number line.


Then we have the $false(x)$ operator. Its codomain looks like this:

$$false(x) = 0^{|x|+x} = \begin{cases} 0 & \text{if } x > 0 \\
1 & \text{if } x \leq   0\end{cases}$$

We can also define the $sign(x)$ function. Its codomain looks like this:

$$sign(x) = (-1)^{T(-x)} = \begin{cases} +1 & \text{if } x \geq   0 \\
-1 & \text{if } x < 0 \end{cases}$$

So next up is to define the basic $not(x)$, $and(x, y)$, and $or(x, y)$.

Let us define: $$not(x) = 1 - true(x)$$

Let us define: $$and(x, y) = true(x) \times true(y)$$

Let us define: $$or(x, y) = not(and(not(x), not(y)))$$

The $max(a, b)$ function can easily be defined using the previous logic operations.

Let us define it as:

$$max(a, b) = a\cdot true\left(a\ -\ b\right)\ +\ b\cdot\left(1\ -\ true\left(a\ -\ b\right)\right)$$

and the $min(a, b)$ function can then just switch the arguments around.

$$min(a, b) = b\cdot true\left(a\ -\ b\right)\ +\ a\cdot\left(1\ -\ true\left(a\ -\ b\right)\right)$$

Greater than:

$$x \gt a = 1-0^{\left|a-\ \max\left(x,\ a\right)\right|}$$

Greater than or equal:

$$x \geq a = 0^{\left|a\ -\ \min\left(x,\ a\right)\right|}$$

Lesser than:

$$x < a = 1-0^{\left|a\ -\ \min\left(x,\ a\right)\right|}$$

Lesser than or equal:

$$x \leq a = 0^{\left|a\ -\ \max\left(x,\ a\right)\right|}$$

... we can go on and on...


Let's do *Greater than*, *Lesser than* / *or equal*.

$$between(x, a, b) = a < x < b = 0^{|true(x-a)-true(-x-b)|}= true(x-a)-0^{|(x - b)|-(x-b)} =\begin{cases} 1 & \text{if } a \lt x \lt b \\ 
0 & \text{else }\end{cases}$$

...or just $(a, b)$ using interval notation.

### Piecewise functions

But now we can do Piecewise functions with "pure" math.

....


### Lagrangian functions

Rectangular function can be defined using the logical operations above. But it's also possible to define it using a logistic function IIF we have defined $\frac{x}{0} = \infty$, and $\frac{x}{\infty} = 0$.

$$rect(x)= \frac{1}{1 + 0^{x + 0.5}} - \frac{1}{1 + 0^{x - 0.5}}$$


----------------------


### notes

TODO: Expand these subject
1. Numerical stability
2. Trigonometry functions
3. Gamma function
4. Numerical Integration



$$\int^{\infty}_{0} t^{z-1}e^{-x}$$

$$N^x\prod^{\infty}_{k=1} \frac{k}{k + x}$$

etc..

