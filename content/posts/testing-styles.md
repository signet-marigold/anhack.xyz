---
title: "Testing Styles"
date: 2023-09-27T14:52:53Z
---



# H1 Title
## H2 Title
### H3 Title
#### H4 Title
##### H5 Title
###### H6 Title

Regular text

![camera lense](https://www.seiu1000.org/sites/main/files/main-images/camera_lense_0.jpeg)
image

[![camera lense](https://www.seiu1000.org/sites/main/files/main-images/camera_lense_0.jpeg)](#image-with-link)
image with link

[internal link](#internal-link)
[external link](http://localhost)

bulleted list
- item 1
- item 2
    - item 1
    - item 2
    - item 3
- item 3

numbered list
1. item 1
1. item 2
    1. item 1
    1. item 2
    1. item 3
1. item 3

ordered numbered list
1. item 1
2. item 2
    1. item 1
    2. item 2
    3. item 3
3. item 3

> right carret
> what does this do?

`backtick`

```tripple backtick```

    indentation

Table
| cat 1 | cat 2 | cat 3 |
|-------|:-----:|------:|
| thing | `heh` | ohno  |

{{< expand "Expand to see Fish" >}}
grumble grumble grumble

![fish](https://www.insidescience.org/sites/default/files/2020-06/Smallfish2_topNteaser.jpg)
{{< /expand >}}

~~strikethough~~

*italics yippee*

**bold**

_underscored wait italics again??_

lots → of → arrows

*≡*

```zsh
zsh block
look at how fun!
```

```sh
sh block
look how boring
```

```yaml
yaml:
    testing:
        how-fun: "weewoo"
```

```text
text block
```

```jsonc
{
    "json-testing": {
        "hell": "yeah"
    }
}
```

```css
css: block;
```

{{< panel info >}}

extra long content that will definatly overflow into the next line haha its so fun to write fluff and extra words all day long asnasjndasjnbdasjkbnajknbglsj

# header test

new line
{{< /panel >}}


{{< panel note >}}note panel{{< /panel >}}
{{< panel example >}}example panel{{< /panel >}}
{{< panel info >}}info panel{{< /panel >}}
{{< panel caution >}}caution panel{{< /panel >}}
{{< panel danger >}}danger panel{{< /panel >}}
{{< panel error >}}error panel{{< /panel >}}

---
__Advertisement :)__

- __[pica](https://nodeca.github.io/pica/demo/)__ - high quality and fast image
  resize in browser.
- __[babelfish](https://github.com/nodeca/babelfish/)__ - developer friendly
  i18n with plurals support and easy syntax.

You will like those projects!

---

# h1 Heading 8-)
## h2 Heading
### h3 Heading
#### h4 Heading
##### h5 Heading
###### h6 Heading


## Horizontal Rules

___

---

***


## Typographic replacements

Enable typographer option to see result.

(c) (C) (r) (R) (tm) (TM) (p) (P) +-

test.. test... test..... test?..... test!....

!!!!!! ???? ,,  -- ---

"Smartypants, double quotes" and 'single quotes'


## Emphasis

**This is bold text**

__This is bold text__

*This is italic text*

_This is italic text_

~~Strikethrough~~


## Blockquotes


> Blockquotes can also be nested...
>> ...by using additional greater-than signs right next to each other...
> > > ...or with spaces between arrows.


## Lists

Unordered

+ Create a list by starting a line with `+`, `-`, or `*`
+ Sub-lists are made by indenting 2 spaces:
  - Marker character change forces new list start:
    * Ac tristique libero volutpat at
    + Facilisis in pretium nisl aliquet
    - Nulla volutpat aliquam velit
+ Very easy!

Ordered

1. Lorem ipsum dolor sit amet
2. Consectetur adipiscing elit
3. Integer molestie lorem at massa


1. You can use sequential numbers...
1. ...or keep all the numbers as `1.`

Start numbering with offset:

57. foo
1. bar


## Code

Inline `code`

Indented code

    // Some comments
    line 1 of code
    line 2 of code
    line 3 of code


Block code "fences"

```
Sample text here...
```

Syntax highlighting

``` js
var foo = function (bar) {
  return bar++;
};

console.log(foo(5));
```

## Tables

| Option | Description |
| ------ | ----------- |
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |

Right aligned columns

| Option | Description |
| ------:| -----------:|
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |


## Links

[link text](http://dev.nodeca.com)

[link with title](http://nodeca.github.io/pica/demo/ "title text!")

Autoconverted link https://github.com/nodeca/pica (enable linkify to see)


## Images

![Minion](https://octodex.github.com/images/minion.png)
![Stormtroopocat](https://octodex.github.com/images/stormtroopocat.jpg "The Stormtroopocat")

Like links, Images also have a footnote style syntax

![Alt text][id]

With a reference later in the document defining the URL location:

[id]: https://octodex.github.com/images/dojocat.jpg  "The Dojocat"


## Plugins

The killer feature of `markdown-it` is very effective support of
[syntax plugins](https://www.npmjs.org/browse/keyword/markdown-it-plugin).


### [Emojies](https://github.com/markdown-it/markdown-it-emoji)

> Classic markup: :wink: :crush: :cry: :tear: :laughing: :yum:
>
> Shortcuts (emoticons): :-) :-( 8-) ;)

see [how to change output](https://github.com/markdown-it/markdown-it-emoji#change-output) with twemoji.


### [Subscript](https://github.com/markdown-it/markdown-it-sub) / [Superscript](https://github.com/markdown-it/markdown-it-sup)

- 19^th^
- H~2~O


### [\<ins>](https://github.com/markdown-it/markdown-it-ins)

++Inserted text++


### [\<mark>](https://github.com/markdown-it/markdown-it-mark)

==Marked text==


### [Footnotes](https://github.com/markdown-it/markdown-it-footnote)

Footnote 1 link[^first].

Footnote 2 link[^second].

Inline footnote^[Text of inline footnote] definition.

Duplicated footnote reference[^second].

[^first]: Footnote **can have markup**

    and multiple paragraphs.

[^second]: Footnote text.




### [Definition lists](https://github.com/markdown-it/markdown-it-deflist)

Term 1

:   Definition 1
with lazy continuation.

Term 2 with *inline markup*

:   Definition 2

        { some code, part of Definition 2 }

    Third paragraph of definition 2.

_Compact style:_

Term 1
  ~ Definition 1

Term 2
  ~ Definition 2a
  ~ Definition 2b


### [Abbreviations](https://github.com/markdown-it/markdown-it-abbr)

This is HTML abbreviation example.

It converts "HTML", but keep intact partial entries like "xxxHTMLyyy" and so on.

*[HTML]: Hyper Text Markup Language

### [Custom containers](https://github.com/markdown-it/markdown-it-container)

::: warning
*here be dragons*
:::



*Some content including images are copyright of GitHub, Inc.*
