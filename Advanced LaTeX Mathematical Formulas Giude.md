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

Example:

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

Example:

$\int\!\!\!\int_D f\,dx\,dy$ - `\int\!\!\!\int_D f\,dx\,dy`

## Changing Math style

| Command              | Effect                        |
| :------------------- | ----------------------------- |
| `\displaystyle`      | Full size (like display math) |
| `\textstyle`         | Inline size                   |
| `\scriptstyle`       | Sub/superscript size          |
| `\scriptscriptstyle` | Smaller                       |

Task force sum limits in inline math

```latex
$\sum_{k=1}^{n} k$                 % limits on side
$\displaystyle\sum_{k=1}^{n} k$    % limits above/below
```

Example:

$$