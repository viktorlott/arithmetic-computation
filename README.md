# Symbolic math

So the goal with this is more to see if it's possible to define certain math operations with just using **Arithmetic operations**, **Algebra rules**, **Series and Sequences**.


> I could not find any information about this subject, anywhere. 
> So much of this "seems" to not have been explored (or even cared about).


> NOTE: There're certain Analytical continuations for certain functions, but that's not the point of this.


### Basics
Let me give you an example. Take the Modulo operator. Its definition includes the Absolute- and the Floor operator. But how are they defined?

The Absolute operator is very simple, we've seen it many times in action. It has this signature, $\sqrt{x^2}$.

Lets define it as: $|x|=\sqrt{x^2}$.

Now, the Floor operator can actually be defined by the Modulo operator. It's a bit tricky, so to define it, we have to use two trigonometry functions. Took me a while to figure this out..

Lets define it as: $mod(x, y) = \frac{y\times\cot^{-1}(\cot(\frac{\pi x}{y}))}{\pi}$.

Lets define: $truncate(x) = mod(x, 1)$

So with this, we can define the Floor operator.

Lets define it as: $\lfloor x \rfloor = x - truncate(x)$.

We can also define the Ceil operator now.

Lets define it as: $\lceil x \rceil = x + truncate(-x)$.

We can also define $Round(x)$, both up and down.

Lets define it as: $RoundUp(x) = \lfloor x + 0.5 \rfloor$.

Lets define it as: $RoundDown(x) = \lceil x - 0.5 \rceil$.


We can now move over to more logical operators. We begin with $True(x)$. Its codomain looks like this.

$
True(x) = 
\begin{cases} 
1 & \text{if } x > 0 \\
0 & \text{if } x \leq   0
\end{cases}
$

Lets define it as: $True(x) = 1 - 0^{|x|+x}$

Then we have the $False(x)$ operator. Its codomain looks like this:

$
False(x) = 
\begin{cases} 
0 & \text{if } x > 0 \\
1 & \text{if } x \leq   0
\end{cases}
$

Lets define it as: $True(x) = 0^{|x|+x}$

We can also define the $Sign(x)$ function. Its codomain looks like this:

$
Sign(x) = 
\begin{cases} 
+1 & \text{if } x \geq   0 \\
-1 & \text{if } x < 0 
\end{cases}
$

Lets define it as: $Sign(x) = (-1)^{1 - F(-x)}$


So next up is to actually define the basic $Not(x)$, $And(x, y)$, And $Or(x, y)$.

Lets define: $Not(x) = 1 - True(x)$.

Lets define: $And(x, y) = True(x) \times True(y)$.

Lets define: $Or(x, y) = Not(And(Not(x), Not(y)))$.

... we can go on and on..


But now we can actually do piecewise functions with "pure" math.

Lets do *Greater than*, *Lesser than* / *or equal*.

$
Between(x, a, b) = 
\begin{cases} 
x & \text{if } a \lt x \lt b \\
0 & \text{else }
\end{cases}
$

...or just $(a, b)$ using interval notation.

Lets define $Between(x, a, b)=x \times (True(x-a)-0^{|(x - b)|-(x-b)})$


----------------------

TODO:
Max(x, y), Min(x, y), Greater[eq](x, y), Lesser[eq](x, y)...
e.g. MycoolFunction(x)*True(x) + ElseCallthis(x)*False(x)





### Notes

TODO: Expand these subject
1. Numerical stability
2. Trigonometry functions
3. Gamma function
4. Numerical Integration



$\int^{\infin}_{0} t^{z-1}e^{-x}$

$N^x\prod^{\infin}_{k=1} \frac{k}{k + x}$

etc..



