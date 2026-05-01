# 1. Essential Packages

Load these in your preamble for full functionality:

```latex
\userpackage{asmath}    % Core math extensions
\userpackage{amssymb}   % Additional symbols
\userpackage{mathtools} % Fixes/extensions for asmath
\userpackage{bm}        % Bold math symbols
```

# 2. Fine-Tuning Spacing and Style

## Manual spaces

| Command | Length                | Example     |
| :------ | --------------------- | ----------- |
| `\,`    | 3/18 quad             | `a\,b`      |
| `\:`    | 4/18 quad             | `a\:b`      |
| `\;`    | 5/18 quad             | `a\;b`      |
| `\quad` | 1 em                  | `a\quad b`  |
| `qquad` | 2 em                  | a`\qquad b` |
| `\!`    | -3/18 quad (negative) | `a\!b`      |

Example: ---

$a\,b$ - `a\,b`                    3/18 quad
$a\:b$ - `a\:b`                    4/18 quad
$a\;b$ - `a\;b`                    5/18 quad
$a\quad b$ - `a\quad b`          1 em
$a \qquad b$ - `a \qquad b`   2 em
$a\!b$ - `a\!b`                      -3/18 (negative)

Use `\!` to tighten integrals or move limits:

```latex
	\int\!\!\!\int_D f\,dx\,dy % double integrals with less space
```

Example: ---

$\int\!\!\!\int_D f\,dx\,dy$ - `\int\!\!\!\int_D f\,dx\,dy`

## Changing Math style

| Command              | Effect                                  |
| :------------------- | --------------------------------------- |
| `\displaystyle`      | Full size (like display math) - default |
| `\textstyle`         | Inline size                             |
| `\scriptstyle`       | Sub/superscript size                    |
| `\scriptscriptstyle` | Smaller                                 |

Task force sum limits in inline math

```latex
$\sum_{k=1}^{n} k$                 % limits on side
$\displaystyle\sum_{k=1}^{n} k$    % limits above/below
```

Example: ---

$\sum_{k=1}^{n} k$ - `\sum_{k=1}^{n} k`                                   Default

$\displaystyle\sum_{k=1}^{n} k$ - `\displaystyle\sum_{k=1}^{n} k`              Display

$\textstyle\sum_{k=1}^{n} k$ - `\textstyle\sum_{k=1}^{n} k`                Text Style

$\scriptstyle\sum_{k=1}^{n} k$ - `\scriptstyle\sum_{k=1}^{n} k`                For Scripts

$\scriptscriptstyle\sum_{k=1}^{n} k$ - `\scriptscriptstyle\sum_{k=1}^{n} k`      Smaller

# 3. Advanced Brackets and Delimiters

## Automatic sizing with `\left` and `\right`

```latex
\left( \frac{a}{b} \right)            % parentheses scale
\left[ \int_0^1 x^2 dx \right]        % brackets scale
\left\{ \begin{pmatrix} 1 & 2 \\ 3 & 4 \end{pmatrix} \right\}
```

Note: Each `\left` needs a `\right`. Use `\left` or `\right`. for an invisible delimiter.

Example: ---

$\left( \frac{a}{b} \right)$ - `\left( \frac{a}{b} \right)`

$\left[ \int_0^1 x^2 dx \right]$ - `\left[ \int_0^1 x^2 dx \right]`

$\left\{ \begin{pmatrix} 1 & 2 \\ 3 & 4 \end{pmatrix} \right\}$  - `\left\{ \begin{pmatrix} 1 & 2 \\ 3 & 4 \end{pmatrix} \right\}`

## Manual sizing

Use `\bigl`, `\Bigl`, `\biggl`, `\Biggl` (and `\bigr` etc.) for better control:

```latex
\bigl( \frac{1}{2} \bigr)    % smaller than \left ( \right)
\Bigl[ \frac{1}{2} \Bigr]
```

Example:  ---

$\bigl( \frac{1}{2} \bigr)$ - `\bigl( \frac{1}{2} \bigr)`

$\Bigl( \frac{1}{2} \Bigr)$ - `\Bigl[ \frac{1}{2} \Bigr]`

## Multi-line delimiters (with `\vphantom`)

```latex
\left( \frac{a}{b} \vphantom{\frac{c}{d}} \right)    % match height
```

Example: ---

$\left( \frac{a}{b} \vphantom{\frac{c}{d}} \right)$ - `\left( \frac{a}{b} \vphantom{\frac{c}{d}} \right)`

# 4. Multi-line Equations

## `align` environment (from `asmath`)

Numbered lines:

```latex
\begin{align}
x &= y + z \\
y &= a^2 + b^2
\end{align}
```

Example: ---

$$
\begin{align}
x &= y + z \\
y &= a^2 + b^2
\end{align}
$$

Remove numbers with `\nonumber` or use `align*`.

Align at multiple points:

```latex
\begin{align}
x &= y       &  a &= b + c \\
z &= w + 1   &  d &= e
\end{align}
```

Example:

$$
\begin{align}
x &= y       &  a &= b + c \\
z &= w + 1   &  d &= e
\end{align}
$$

## `split` for one equation spanning lines (single number)

```latex
\begin{equation}
\begin{split}
f(x) &= (x+1)^2 \\
     &= x^2 + 2x + 1
\end{split}
\end{equation}
```

$$
\begin{equation}
\begin{split}
f(x) &= (x+1)^2 \\
     &= x^2 + 2x + 1
\end{split}
\end{equation}
$$

## `cases` for piecewise definitions

```latex
f(x) = \begin{cases}
x^2, & x < o \\
e^x, & x \ge 0
\end{cases}
```

$$
f(x) = \begin{cases}
x^2, & x < o \\
e^x, & x \ge 0
\end{cases}
$$

With `mathtools` you get `\dcases` (display style) and `\cases*` {text second column}.

## `gathered` for vertical centering

```latex
\begin{equation}
\begin{gathered}
a = b + c \\
x = y
\end{gathered}
\end{equation}
```

$$
\begin{equation}
\begin{gathered}
a = b + c \\
x = y
\end{gathered}
\end{equation}
$$

# 5. Advanced Limits, Sums, and Integrals

## Subscriptions under operators: `\substack`

```latex
\sum_{\substack{1\le i\le n \\ i\ne j}} a_{i}
```

Example: ---

$\sum_{\substack{1\le i\le n \\ i\ne j}} a_{i}$ - `\sum_{\substack{1\le i\le n \\ i\ne j}} a_{i}`

## Multiple limits: `\sideset` (for things like primers on sums)

```latex
\sideset{}{'}\sum_{n=1}^\infty a_n    % a prime after the sum
```

Example: ---

$\sideset{}{'}\sum_{n=1}^\infty a_n$ - `\sideset{}{'}\sum_{n=1}^\infty a_n`

## Over - and under-scripts on any symbol: `\overset`, `\underset`

```latex
\overset{*}{X} \quad \underset{\text{def}}{=}
```

Example: ---

$\overset{*}{X} \quad \underset{\text{def}}{=}$ - \overset{*}{X} \quad \underset{\text{def}}{=}

## `\mathclap` for tight spacing (from `mathtools`)

```latex
\sum_{\mathclap{1\le i\le n}} a_i    % no extra horizontal space
```

$\sum_{\mathclap{1\le i\le n}} a_i$ - \sum_{\mathclap{1\le i\le n}} a_i

## Integrals with limits

```latex
\oint_C F\cdot dr \qquad \iint_D dx\,dy
```

Example: ---

$\oint_C F\cdot dr \qquad \iint_D dx\,dy$ - `\oint_C F\cdot dr \qquad \iint_D dx\,dy`

Use `\substack` on multiple integrals limits:

```latex
\int\limits_{\substack{x>0 \\ y>0}} f{x,y}\,dx\,dy
```

$\int\limits_{\substack{x>0 \\ y>0}} f{x,y}\,dx\,dy$ - `\int\limits_{\substack{x>0 \\ y>0}} f{x,y}\,dx\,dy`

# 6. Matrices

## Standard matrices (from `asmath`)

```latex
\begin{pmatrix} a & b \\ c & d \end{pmatrix} % parentheses
\begin{bmatrix} a & b \\ c & d \end{bmatrix} % brackets
\begin{Bmatrix} a & b \\ c & d \end{Bmatrix} % braces
\begin{vmatrix} a & b \\ c & d \end{vmatrix} % single bars
\begin{Vmatrix} a & b \\ c & d \end{Vmatrix} % double bars
```

Example: ---

$$
\begin{pmatrix} a & b \\ c & d \end{pmatrix}
\begin{bmatrix} a & b \\ c & d \end{bmatrix}
\begin{Bmatrix} a & b \\ c & d \end{Bmatrix}
\begin{vmatrix} a & b \\ c & d \end{vmatrix}
\begin{Vmatrix} a & b \\ c & d \end{Vmatrix}
$$

## Custom alignment with `array`

```latex
\left( \begin{array}{c|c}
a & b \\ \hline
c & d
\end{array} \right)
```

Example: ---

$$
\left( \begin{array}{c|c}
a & b \\ \hline
c & d
\end{array} \right)
$$

## Dotted matrices

Use `\cdots`, `\ddots`, `\vdots` inside `matrix`:

```latex
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{pmatrix}
```

Example ---

$$
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{pmatrix}
$$

# 7. Text inside Math

## `\text` (from `asmath`) - adapts to current style

```latex
f(x) = \text{the function } x^2 \text{ for } x>0
```

Example: ---

$f(x) = \text{the function } x^2 \text{ for } x>0$ - `f(x) = \text{the function } x^2 \text{ for } x>0`

## `\textup`, `textit`, etc. for explicit font

```latex
\lim_{x\to 0} \text{(by continuty)} f(x)
```

Example: ---

$\lim_{x\to 0} \text{(by continuty)} f(x)$ - `\lim_{x\to 0} \text{(by continuty)} f(x)`

## `\intertext` to insert text between aligned equations

```latex
\begin{align*}
A &= B \\
\intertext{and by the lemma we have}
B &= C
\end{align*}
```

# 8. Symbols and Fonts

## Blackboard bold (ℕ, ℝ, ℂ, …)

```latex
\mathbb{N} \quad \mathbb{R} \quad \mathbb{C}
```

Example: ---

$\mathbb{N} \quad \mathbb{R} \quad \mathbb{C}$ - `\mathbb{N} \quad \mathbb{R} \quad \mathbb{C}`

## Calligraphic (𝒜, ℬ, …)

```latex
\mathcal{A} \quad \mathcal{B}
```

Example: ---

$\mathcal{A} \quad \mathcal{B}$ - \mathcal{A} \quad \mathcal{B}

## Fraktur (𝔄, 𝔅, …)

```latex
\mathfrak{A} \quad \mathfrak{B}
```

Example: ---

$\mathfrak{A} \quad \mathfrak{B}$ - `\mathfrak{A} \quad \mathfrak{B}`

## Bold symbols (for vectors, matrices)

```latex
\mathbf{x} \quad \bm{\alpha}    % \bm from bm package ()
```