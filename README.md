# The Fundamental Theorem of Calculus

### What it says, why it's true, and why it *has* to be true

---

## 1. Setting the Stage

Calculus is built from two seemingly unrelated ideas:

- **Differentiation** — the study of *instantaneous rates of change* (slopes of tangent lines).
- **Integration** — the study of *accumulated quantities* (areas under curves).

For centuries these were treated as separate problems. The Fundamental Theorem of Calculus (FTC) is the discovery that they are **inverse operations** — two sides of the same coin. This is one of the most important results in all of mathematics, because it turns the (hard, geometric) problem of computing an area into the (easy, algebraic) problem of finding an antiderivative.

---

## 2. Statement of the Theorem

Let $f$ be continuous on $[a, b]$.

### Part 1 (The Accumulation Function is an Antiderivative)

Define

$$
F(x) = \int_a^x f(t)\, dt, \qquad x \in [a,b].
$$

Then $F$ is differentiable on $[a,b]$ and

$$
F'(x) = f(x).
$$

### Part 2 (Evaluation Theorem)

If $F$ is *any* antiderivative of $f$ (i.e. $F' = f$) on $[a,b]$, then

$$
\int_a^b f(x)\, dx = F(b) - F(a).
$$

This second statement is the one your question is really about. Let's unpack it carefully, because the way it's usually written hides the beautiful idea inside it. Rewrite it using $f = F'$:

$$
\boxed{\;F(b) - F(a) = \int_a^b F'(x)\, dx\;}
$$

**In words:** *the total change in a function over an interval equals the area under its derivative over that same interval.*

This is the heart of what you're asking about. Let's build up to understanding *why this must be true* from three different angles: a logical/dimensional angle, an analytical (proof-based) angle, and a geometric/constructive angle.

---

## 3. Why It *Should* Be True — The Logical Perspective

### 3.1 The "speedometer and odometer" argument

Suppose $F(x)$ tracks your **position** on a road at time $x$. Then $F'(x)$ is your **velocity** — what your speedometer reads at time $x$.

Ask yourself: *how far did you travel between time $a$ and time $b$?*

There are two ways to answer this:

1. **Look at the odometer.** Distance traveled $= F(b) - F(a)$ — just subtract the start reading from the end reading. You don't need to know anything about *how* you got there.
2. **Look at the speedometer over time.** If you know your velocity $F'(x)$ at every instant, you can recover total distance by "summing up" all the tiny distances $F'(x)\, dx$ you covered in each infinitesimal moment $dx$. That sum, in the limit, is $\int_a^b F'(x)\,dx$.

These are two completely different ways of measuring the *same physical quantity* — total distance traveled. There is no reason they should disagree, because they are not two different facts about the world; they are two different bookkeeping methods for the **same** fact. The FTC is simply the mathematical statement that these two bookkeeping methods must agree.

This is why the theorem should be true *before you ever prove it*: **the derivative encodes the rate of change, and the integral is defined precisely as the machine that reverses rate-of-change back into total change.** Differentiation zooms in and asks "how fast right now?" Integration zooms back out and asks "how much in total?" They are inverse questions about the same underlying process.

### 3.2 The telescoping-sum argument (the real engine of the theorem)

Here is the key logical trick that makes the "should be true" intuition rigorous. It relies on nothing more than algebra.

Chop $[a,b]$ into $n$ tiny pieces using points

$$
a = x_0 < x_1 < x_2 < \cdots < x_n = b.
$$

Now write $F(b) - F(a)$ as a **telescoping sum** — a chain where each term cancels with the next, leaving only the ends:

$$
F(b) - F(a) = \sum_{i=1}^{n} \big[F(x_i) - F(x_{i-1})\big].
$$

This is just algebra: $[F(x_1)-F(x_0)] + [F(x_2)-F(x_1)] + \cdots + [F(x_n)-F(x_{n-1})]$. Every interior term appears once with a $+$ and once with a $-$, so it all collapses back to $F(x_n) - F(x_0) = F(b)-F(a)$. **No calculus has been used yet** — this identity is true for *any* function $F$, continuous or not.

Now bring in calculus. Each little piece $F(x_i) - F(x_{i-1})$ is the change in $F$ over a *tiny* interval $[x_{i-1}, x_i]$. But over a tiny interval, the derivative $F'$ barely changes, so $F$ behaves almost exactly like a straight line with slope $F'(x_i^*)$ for some point $x_i^*$ in that piece. This gives (and the Mean Value Theorem below makes this exact, not approximate):

$$
F(x_i) - F(x_{i-1}) \approx F'(x_i^*)\,(x_i - x_{i-1}).
$$

Substituting into the telescoping sum:

$$
F(b) - F(a) = \sum_{i=1}^n F(x_i)-F(x_{i-1}) \approx \sum_{i=1}^n F'(x_i^*)\, \Delta x_i.
$$

But look at the right-hand side — that is *exactly* the Riemann sum that defines $\int_a^b F'(x)\,dx$! As $n \to \infty$ and each $\Delta x_i \to 0$, the approximation becomes exact and the sum converges to the integral. Hence:

$$
F(b) - F(a) = \int_a^b F'(x)\, dx.
$$

**This is the logical core of the entire theorem.** The reason the "total change" equals the "area under the derivative" is that:

- Total change can *always* be broken into a telescoping sum of small changes (pure algebra).
- Each small change is *approximately* slope $\times$ width, because a differentiable function looks locally linear (this is the very meaning of "derivative").
- Summing "slope $\times$ width" pieces and taking the limit is, by definition, exactly what a definite integral computes (area under the curve = sum of thin rectangle areas, height $\times$ width).

So the FTC isn't a coincidence bridging two unrelated fields — it is what you get when you take the definition of a derivative (local linearity) and glue infinitely many of these local pieces together using nothing but the telescoping-sum trick. **Local linear approximation, summed up globally, reconstructs the whole.**

---

## 4. Why It *Is* True — The Analytical / Rigorous Perspective

The heuristic above becomes a real proof once we replace "$\approx$" with an exact statement — supplied by the **Mean Value Theorem (MVT)**.

### 4.1 Proof of Part 2, given Part 1

**Mean Value Theorem.** If $F$ is continuous on $[x_{i-1}, x_i]$ and differentiable on $(x_{i-1}, x_i)$, then there exists some point $x_i^* \in (x_{i-1}, x_i)$ such that

$$
F'(x_i^*) = \frac{F(x_i) - F(x_{i-1})}{x_i - x_{i-1}}.
$$

This isn't an approximation — it is an *exact equality* for some particular point $x_i^*$ inside the subinterval. Rearranged:

$$
F(x_i) - F(x_{i-1}) = F'(x_i^*)\,\Delta x_i \quad \text{exactly}.
$$

Now redo the telescoping sum, but this time with no approximation:

$$
F(b) - F(a) = \sum_{i=1}^n \big[F(x_i)-F(x_{i-1})\big] = \sum_{i=1}^n F'(x_i^*)\, \Delta x_i.
$$

The right-hand side is a genuine Riemann sum for $f = F'$, using the specific sample points $x_i^*$ guaranteed by the MVT. Since $f$ is continuous (hence Riemann-integrable), *every* Riemann sum — regardless of which sample points are used — converges to the same limit as the mesh size $\max \Delta x_i \to 0$:

$$
\lim_{n\to\infty} \sum_{i=1}^n F'(x_i^*)\, \Delta x_i = \int_a^b F'(x)\, dx.
$$

But the left-hand side, $F(b)-F(a)$, doesn't depend on $n$ at all — it's a fixed constant. A sequence of numbers that is constant and also converges to $\int_a^b F'(x)\,dx$ must simply *equal* that integral. Hence:

$$
F(b) - F(a) = \int_a^b F'(x)\, dx = \int_a^b f(x)\,dx. \qquad \blacksquare
$$

### 4.2 Proof of Part 1 (why the accumulation function's derivative gives back $f$)

Define $F(x) = \int_a^x f(t)\,dt$. We compute $F'(x)$ directly from the definition of a derivative:

$$
F'(x) = \lim_{h \to 0} \frac{F(x+h) - F(x)}{h} = \lim_{h\to 0} \frac{1}{h}\int_x^{x+h} f(t)\, dt.
$$

Since $f$ is continuous, on the tiny interval $[x, x+h]$ the value of $f$ is close to $f(x)$ (this is exactly what continuity means). By the **Extreme Value Theorem**, $f$ attains a min $m_h$ and max $M_h$ on $[x,x+h]$, and both $m_h, M_h \to f(x)$ as $h \to 0$. Bounding the integral between rectangles:

$$
m_h \cdot h \;\le\; \int_x^{x+h} f(t)\,dt \;\le\; M_h \cdot h
\quad\Longrightarrow\quad
m_h \;\le\; \frac{1}{h}\int_x^{x+h} f(t)\, dt \;\le\; M_h.
$$

Squeezing $h \to 0$ forces both bounds to $f(x)$, so by the **Squeeze Theorem**:

$$
F'(x) = f(x). \qquad \blacksquare
$$

Intuitively: the *rate* at which area accumulates under a curve, at a given point $x$, is simply the height of the curve at that point — because for an infinitesimally thin sliver, "area added per unit width" *is* the height.

---

## 5. Why It *Should* Be True — The Geometric Perspective

Picture the graph of $F'(x) = f(x)$, and picture the area under it between $a$ and $b$.

- **Cut the interval $[a,b]$ into thin strips** of width $\Delta x$.
- The area of the strip at position $x_i$ is approximately (height)(width) $= f(x_i)\,\Delta x = F'(x_i)\,\Delta x$.
- But $F'(x_i)\,\Delta x$ is *precisely* the amount by which $F$ changes as you move across that strip — because the derivative is defined as "change in $F$ per unit change in $x$," so over a small step $\Delta x$, the change in $F$ is (rate)$\times$(step size).
- **Adding up all the strip areas is therefore the same operation as adding up all the small changes in $F$** across the whole interval.
- Adding up all the small changes in $F$ across $[a,b]$ just gives you the total, net change: $F(b) - F(a)$ — everything in between cancels via telescoping, exactly as in Section 3.2.

So geometrically: **the area under the derivative's graph is not a coincidental match to the total change in the original function — it is a different way of visualizing the exact same accumulation process.** Every rectangle of area under $f=F'$ literally *is* a piece of the total change in $F$, just drawn as a rectangle instead of written as a difference.

This is why swapping the words "area under the derivative" and "total change in the function" feels natural once you see it: they're not two facts that happen to agree, they are **two descriptions of one construction**.

---

## 6. A Concrete Worked Example

Let $F(x) = x^2$, so $F'(x) = 2x$. Take the interval $[1, 3]$.

**Odometer method (just subtract):**

$$
F(3) - F(1) = 9 - 1 = 8.
$$

**Speedometer method (area under the derivative):**

$$
\int_1^3 2x\, dx = \Big[x^2\Big]_1^3 = 9 - 1 = 8.
$$

Both give $8$ — not by coincidence, but because they are two computations of the identical quantity: the net change in $F$ across $[1,3]$.

Geometrically, $\int_1^3 2x\,dx$ is the area of the trapezoid under the line $y = 2x$ from $x=1$ to $x=3$ — with parallel sides of height $2$ and $6$ and width $2$:

$$
\text{Area} = \frac{(2+6)}{2}\cdot 2 = 8.
$$

This trapezoid's area is nothing but $F(3)-F(1)$ redrawn as a picture.

---

## 7. Summary: Three Lenses, One Idea

| Perspective | Core idea |
|---|---|
| **Logical (speedometer/odometer)** | Total change and accumulated rate are two bookkeeping methods for the same physical quantity — they must agree. |
| **Logical (telescoping sum)** | Total change algebraically decomposes into a chain of small changes; small changes are (slope)$\times$(width) by definition of derivative; summing those is exactly what an integral means. |
| **Analytical (MVT proof)** | The Mean Value Theorem makes "small change $\approx$ slope $\times$ width" *exact*, converting the telescoping sum into a genuine Riemann sum that equals the integral in the limit. |
| **Geometric** | Each rectangle of area under $f = F'$ *is* a small change in $F$; summing the areas *is* summing the changes, which telescopes to $F(b)-F(a)$. |

The Fundamental Theorem of Calculus works because **a derivative is a "rate of change," and an integral is the machine built to undo that — to take an infinite collection of infinitesimal rates and reassemble them into the total, accumulated change.** Differentiation breaks a function into infinitesimal pieces of information (slopes); integration is the precise inverse operation of gluing those infinitesimal pieces back together. That total, once reassembled, cannot be anything other than the net difference between where you started and where you ended up — $F(b) - F(a)$.
