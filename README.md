# The Fundamental Theorem of Calculus

### What it says, why it's true, and why it kind of *has* to be true

---

## 1. Setting the stage

Calculus is basically built from two ideas that seem, at first, to have nothing to do with each other.

- **Differentiation**: how fast is something changing right now? (slopes, tangent lines)
- **Integration**: how much has accumulated in total? (area under a curve)

For a long time people treated these as separate problems. The big discovery of the Fundamental Theorem of Calculus (FTC) is that they're actually inverse operations of each other. That's a huge deal, because it means we can compute a hard geometric thing (area) using an easy algebraic thing (an antiderivative), instead of chopping curves into a million rectangles by hand.

---

## 2. What the theorem actually says

Let $f$ be continuous on $[a, b]$.

### Part 1: the accumulation function is an antiderivative

Define

$$
F(x) = \int_a^x f(t)\, dt, \qquad x \in [a,b].
$$

Then $F$ is differentiable and

$$
F'(x) = f(x).
$$

### Part 2: the evaluation theorem

If $F$ is any antiderivative of $f$ (so $F' = f$), then

$$
\int_a^b f(x)\, dx = F(b) - F(a).
$$

This second part is really what your question is about. Let's rewrite it using $f = F'$:

$$
\boxed{\;F(b) - F(a) = \int_a^b F'(x)\, dx\;}
$$

In plain English: the total change in a function over an interval equals the area under its derivative over that same interval. Let's actually dig into why that should be true, then why it is true, then a picture of why it's true.

---

## 3. Why it should be true (the logical angle)

### 3.1 The speedometer and odometer story

Say $F(x)$ is your position on a road at time $x$. Then $F'(x)$ is your velocity, what your speedometer reads at time $x$.

Now ask: how far did you travel between time $a$ and time $b$? You can answer this two different ways.

1. **Check the odometer.** Distance traveled is just $F(b) - F(a)$. Subtract the start reading from the end reading and you're done. You don't need to know anything about how the trip went, just where you started and where you ended.
2. **Check the speedometer the whole time.** If you know your velocity $F'(x)$ at every single instant, you can add up all the tiny bits of distance $F'(x)\, dx$ you covered in each little moment. In the limit that sum is $\int_a^b F'(x)\,dx$.

These are two totally different-looking calculations, but they're measuring the exact same thing: total distance traveled. There's no reason they'd disagree with each other, because they're not two separate facts about the world, they're two ways of bookkeeping one fact. That's basically what the FTC says: these two bookkeeping methods have to agree.

So before we even prove anything, this is why the theorem feels like it has to be true. A derivative tells you a rate of change. An integral is defined as the tool that undoes a rate of change and turns it back into a total. So of course "total change" and "area under the rate" line up. They're describing the same accumulation, just from two directions.

### 3.2 The telescoping sum (this is really the heart of it)

Here's the trick that turns that intuition into something solid, and it only uses algebra.

Chop up $[a,b]$ into $n$ small pieces:

$$
a = x_0 < x_1 < x_2 < \cdots < x_n = b.
$$

Now here's a simple observation. We can write $F(b) - F(a)$ as a telescoping sum:

$$
F(b) - F(a) = \sum_{i=1}^{n} \big[F(x_i) - F(x_{i-1})\big].
$$

This is just bookkeeping: $[F(x_1)-F(x_0)] + [F(x_2)-F(x_1)] + \cdots + [F(x_n)-F(x_{n-1})]$. Every middle term shows up once as a plus and once as a minus, so it all cancels except the very first and very last term, leaving $F(x_n) - F(x_0) = F(b) - F(a)$. Notice we haven't used any calculus yet. This is true for literally any function $F$.

Now let's bring calculus in. Each piece $F(x_i) - F(x_{i-1})$ is the change in $F$ over a tiny little interval. Over a small enough interval, $F$ looks almost like a straight line, with slope roughly $F'(x_i^*)$ for some point $x_i^*$ in that piece. So roughly:

$$
F(x_i) - F(x_{i-1}) \approx F'(x_i^*)\,(x_i - x_{i-1}).
$$

Plug that into the telescoping sum:

$$
F(b) - F(a) \approx \sum_{i=1}^n F'(x_i^*)\, \Delta x_i.
$$

Take a look at the right side. That's exactly a Riemann sum, the thing that defines $\int_a^b F'(x)\,dx$. As we chop the interval into more and more pieces, the approximation gets better and better, and in the limit:

$$
F(b) - F(a) = \int_a^b F'(x)\, dx.
$$

That's really the whole idea. The reason "total change" equals "area under the derivative" comes down to three simple facts stacked on top of each other:

- Any total change can be broken into a chain of small changes that telescopes back to the total. That's just algebra.
- Each small change is approximately slope times width, because that's basically what it means for a function to be differentiable, it looks like a straight line up close.
- Adding up a bunch of "slope times width" pieces and taking a limit is literally the definition of a definite integral.

So the FTC isn't some weird coincidence linking two unrelated branches of math. It's what falls out naturally once you take "a derivative means locally linear" and glue infinitely many of those tiny linear pieces back together using the telescoping trick.

---

## 4. Why it is true (the actual proof)

The argument above works, but it has one soft spot: that "$\approx$" sign. We can make it exact using the **Mean Value Theorem (MVT)**.

### 4.1 Proving part 2, assuming part 1

**MVT:** if $F$ is continuous on $[x_{i-1}, x_i]$ and differentiable on the open interval, then there's some point $x_i^*$ in between where

$$
F'(x_i^*) = \frac{F(x_i) - F(x_{i-1})}{x_i - x_{i-1}}.
$$

This isn't an approximation anymore, it's an exact equality for some specific $x_i^*$. Rearranging:

$$
F(x_i) - F(x_{i-1}) = F'(x_i^*)\,\Delta x_i, \quad \text{exactly}.
$$

Redo the telescoping sum with this exact version:

$$
F(b) - F(a) = \sum_{i=1}^n \big[F(x_i)-F(x_{i-1})\big] = \sum_{i=1}^n F'(x_i^*)\, \Delta x_i.
$$

The right side is a genuine Riemann sum for $f = F'$, using whatever sample points the MVT happened to give us. Since $f$ is continuous, it's integrable, and every Riemann sum converges to the same value as the pieces get smaller, no matter which sample points you use:

$$
\lim_{n\to\infty} \sum_{i=1}^n F'(x_i^*)\, \Delta x_i = \int_a^b F'(x)\, dx.
$$

But look at the left side, $F(b) - F(a)$. It doesn't change no matter how we chop up the interval, it's just a fixed number. A fixed number that also happens to be the limit of a sequence has to equal that limit. So:

$$
F(b) - F(a) = \int_a^b F'(x)\, dx = \int_a^b f(x)\,dx. \qquad \blacksquare
$$

### 4.2 Proving part 1

Define $F(x) = \int_a^x f(t)\,dt$. Take the derivative directly from the definition:

$$
F'(x) = \lim_{h \to 0} \frac{F(x+h) - F(x)}{h} = \lim_{h\to 0} \frac{1}{h}\int_x^{x+h} f(t)\, dt.
$$

Since $f$ is continuous, on the tiny interval $[x, x+h]$ the values of $f$ are all really close to $f(x)$, that's basically what continuity means. Let $m_h$ and $M_h$ be the min and max of $f$ on that little interval. Then

$$
m_h \cdot h \;\le\; \int_x^{x+h} f(t)\,dt \;\le\; M_h \cdot h
\quad\Longrightarrow\quad
m_h \;\le\; \frac{1}{h}\int_x^{x+h} f(t)\, dt \;\le\; M_h.
$$

As $h \to 0$, both $m_h$ and $M_h$ get squeezed toward $f(x)$, so by the squeeze theorem:

$$
F'(x) = f(x). \qquad \blacksquare
$$

The intuitive version: the rate at which area is piling up under a curve at a point $x$ is just the height of the curve at $x$. If you're adding a super thin sliver of area, "area added per unit of width" is just the height of that sliver.

---

## 5. Why it should be true (the picture version)

Picture the graph of $F' = f$, and picture the area under it between $a$ and $b$.

Cut that interval into thin strips of width $\Delta x$. The area of the strip near $x_i$ is roughly height times width, so $f(x_i)\,\Delta x = F'(x_i)\,\Delta x$.

But $F'(x_i)\,\Delta x$ is also exactly how much $F$ changes as you move across that strip. That's what a derivative means, "rate times a small step" gives you the change over that step.

So adding up all those tiny strip areas is literally the same thing as adding up all the tiny changes in $F$ across the whole interval. And adding up all the tiny changes in $F$ just gives you the net change, $F(b) - F(a)$, since everything in between cancels out the same way it did in the telescoping sum.

So here's the punchline: the area under the derivative's graph isn't some separate quantity that happens to match the total change in the original function. It's the same accumulation, just drawn as rectangles instead of written as a subtraction. Every little rectangle under $f = F'$ literally is a piece of the total change in $F$.

---

## 6. A quick example

Let $F(x) = x^2$, so $F'(x) = 2x$. Take $[1,3]$.

**Odometer method (just subtract):**

$$
F(3) - F(1) = 9 - 1 = 8.
$$

**Speedometer method (area under the derivative):**

$$
\int_1^3 2x\, dx = \Big[x^2\Big]_1^3 = 9 - 1 = 8.
$$

Same answer, and not by luck. Both are computing the exact same quantity, the net change in $F$ over $[1,3]$.

Geometrically, $\int_1^3 2x\,dx$ is just the area of the trapezoid under the line $y=2x$ from $x=1$ to $x=3$, with heights $2$ and $6$ and width $2$:

$$
\text{Area} = \frac{(2+6)}{2}\cdot 2 = 8.
$$

That trapezoid is nothing but $F(3) - F(1)$ drawn as a shape instead of written as a subtraction.

---

## 7. Wrapping it up

| Angle | Core idea |
|---|---|
| Speedometer and odometer | Total change and accumulated rate are just two ways of measuring the same thing, so of course they match. |
| Telescoping sum | Total change breaks into a chain of small changes. Each small change is slope times width, since that's what "derivative" means locally. Summing those pieces and taking a limit is exactly what an integral is. |
| MVT proof | The Mean Value Theorem turns "small change is roughly slope times width" into an exact statement, so the telescoping sum becomes an actual Riemann sum equal to the integral. |
| Picture | Each rectangle of area under $f = F'$ is a small change in $F$, so summing the rectangles sums the changes, which telescopes to $F(b) - F(a)$. |

At the end of the day, the FTC works because a derivative is just a rate of change, and an integral is the tool built specifically to undo that, to take a bunch of infinitely small rates and glue them back together into the total change. Differentiation chops a function up into tiny pieces of information about its slope. Integration is the reverse process, gluing those pieces back together. And once you glue them all back together, what you get can't be anything other than the difference between where the function started and where it ended up, $F(b) - F(a)$.
