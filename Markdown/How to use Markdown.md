## Tables --- !

You can make tables for the followed instructions:

```text
| Header 1 | Header 2 | Header 3|
| :--- | :---: | ---: |
| Left aligment | Center aligment | Right aligment |
| `code` | **fat** | [Link](url) |
```

Example:

| Header 1       |     Header 2     |        Header 3 |
| :------------- | :--------------: | --------------: |
| Left alignment | Center alignment | Right alignment |
| `code`         |     **fat**      |        [Link]() |

`:---`   - the left alignment for the all column
`:---:` - the center alignment for the all column
`---:`   - the right alignment for the all column

the `|` char used for separating the columns
the `-` char used for separating the headers  from the data

For the advanced tables usually use special addons for Markdown, like the `markdovn-it-adv-table` for creating a more difficult structures

## Video pasting --- !

For pasting video to the Markdown document, usually use the `<iframe>` HTML-tag

Direct embedding using `<iframe>` (dose not work everywhere):

```html
<iframe width="560" height="315" src="https://www.youtube.com/embed/ID_ВИДЕО" title="YouTube video player" frameborder="0" allowfullscreen></iframe>
```

Example:
<iframe width="900" height="500" src="https://www.youtube.com/embed/9nFBnro15vY?list=RDGMEMhCgTQvcskbGUxqI4Sn2QYw" title="Maybe This Year ft. Hatsune Miku and Megurine Luka" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
### - Alternative ways:

#### Image-Link: 

A very reliable method. You make the screenshot-video (or will getting its preview), and make this to the clickable-link, that is way you to YouTube:

```text
[![Alt text](way_to_preview.jpg)](https://youtu.be/VIDEO_ID)
```

Example:

**bitbreaker - God Only Knows ft. Kasane Teto**
[![Alt text](YouTubeVideo_01.png)](https://youtu.be/VYsCybhn0s?list=RDGMEMhCgTQvcskbGUxqI4Sn2QYw](https://www.youtube.com/watch?v=_VYsCybhn0s&list=RDGMEMhCgTQvcskbGUxqI4Sn2QYw&index=22))
## Work with Images

Base syntax: `![Alt_text](way_to_the_image)`

Example:

![Some image|697](SomeImage_01.png)

Change parameters:

```html
<img src="imagae.jpg" alt="Описание" width="300" height="200">
```

ex:

<img src="SomeImage_01.png" alt="Description" width="300" height="200">

HAHAHAHAH TRVERSE TETO HAHAHAH!

Adding additional description header:

```html
<figure>
  <img src="image.jpg" alt="Описание">
  <figcaption>Подпись к изображению</figcaption>
</figure>
<img src="img1.jpg" width="48%"> <img src="img2.jpg" width="48%">
```

## Visualization from Mermaid: Diagrams like code

This is the most popular feature advanced Markdown
Mermaid allows you to explaining difficult themes like diagrams with simple text inside the code blocks

This is a best way to represent difficult code or architecture

- Block-scheme  (Flowchart): for **`process representation`**
- Diagram of sequence (Sequence Diagram): for representation **`object interactions in time`**
- Gant Diagram (Gantt Chart): for schedules,  deadlines etc. visualization

## Text and code design

### - Code Syntax highlighting:

```text
'''javascript
function hello() {
	console.log("Hello world!");
}
'''
```

ex:

```javascript
function hello() {
	console.log("Hello world!");
}
```

### - Tasks List:

```text
- [ ]
- [x]
- [x]
```

Where:
- `[ ]` - current task
- x - finished task

ex:

- [x] Learn English
- [ ] learn Proper Noun

## Mathematical formulas

For the science and tech texts, you may use the LaTeX formulas in Markdown editors

- Insides formulas: boxed in the single $ chars `$E = mc^2$`
- Selected formulas: boxed in the double $ chars and align to center themself

ex:

$E = mc^2$
$$
\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}
$$


