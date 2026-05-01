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