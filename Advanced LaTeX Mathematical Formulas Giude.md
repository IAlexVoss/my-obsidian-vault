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

Use `\!` to tighten integrals or move limits:

```latex
	\int\!\!\!\int_D f\,dx\,dy % double integrals
```