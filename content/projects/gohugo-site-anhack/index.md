---
title: "This GoHugo Site"
subtitle: "How I made a custom blog"
date: 2024-02-08T23:53:06-06:00
lastMod: 2024-02-08T23:53:06-06:00
author: ""
image: "gohugo-site-anhack-banner.png"
imageAlt: ""
category: ""
tags: ["web"]
toc: true
draft: true
---

## hugo structure

### overview

Here is the hugo project structure.

```render
Project Root
.
├── archetypes{{< footnote title="1" target="project-tree-ref-1" >}}
│   ├── default.md{{< footnote title="1a" target="project-tree-ref-2" >}}
│   ├── posts{{< footnote title="1b" target="project-tree-ref-3" >}}
│   └── projects
├── assets{{< footnote title="4" target="project-tree-ref-4" >}}
│   └── images
├── config.toml{{< footnote title="5" target="project-tree-ref-5" >}}
├── content
│   ├── _index.md
│   ├── posts
│   ├── projects
│   └── recipes
├── data
├── deploy{{< footnote title="6" target="project-tree-ref-6" >}}
├── layouts{{< footnote title="7" target="project-tree-ref-7" >}}
│   ├── index.html{{< footnote title="8" target="project-tree-ref-8" >}}
│   ├── partials{{< footnote title="9" target="project-tree-ref-9" >}}
│   └── robots.txt{{< footnote title="10" target="project-tree-ref-10" >}}
├── static{{< footnote title="11" target="project-tree-ref-11" >}}
│   ├── badges
│   ├── icons
│   └── img
└── themes
    └── asperity{{< footnote title="12" target="project-tree-ref-12" >}}
        ├── archetypes
        ├── assets
        │   ├── css
        │   ├── js
        │   └── scss
        │       ├── components{{< footnote title="13" target="project-tree-ref-13" >}}
        │       ├── css
        │       │   └── normalize.css{{< footnote title="14" target="project-tree-ref-14" >}}
        │       ├── fonts
        │       │   ├── noto-sans
        │       │   │   └── <font parts>
        │       │   └── _noto-sans.scss (font collection)
        │       ├── _*.scss{{< footnote title="15" target="project-tree-ref-15" >}}
        │       ├── fonts.scss{{< footnote title="16" target="project-tree-ref-16" >}}
        │       └── main.scss{{< footnote title="17" target="project-tree-ref-17" >}}
        ├── i18n{{< footnote title="18" target="project-tree-ref-18" >}}
        ├── layouts{{< footnote title="19" target="project-tree-ref-19" >}}
        │   ├── _default{{< footnote title="20" target="project-tree-ref-20" >}}
        │   ├── partials{{< footnote title="21" target="project-tree-ref-21" >}}
        │   └── shortcodes{{< footnote title="22" target="project-tree-ref-22" >}}
        ├── static{{< footnote title="23" target="project-tree-ref-23" >}}
        │   ├── 40{x}.html{{< footnote title="24" target="project-tree-ref-24" >}}
        │   ├── css{{< footnote title="25" target="project-tree-ref-25" >}}
        │   ├── fonts
        │   ├── icons
        │   └── img
        ├── config.toml{{< footnote title="26" target="project-tree-ref-26" >}}
        └── theme.toml{{< footnote title="27" target="project-tree-ref-27" >}}
```

#### references

##### ref 1: Archetypes store the new page templates {#project-tree-ref-1}

Which looks something like this

```toml
---
date: {{ .Date }}
title: "{{ replace .Name "-" " " | title }}"
subtitle: ""
author: ""
image: ""
tags: []
---
```

##### ref 1a: Used if you run new on a main directory (e.g. new posts/new-post.md) {#project-tree-ref-2}
##### ref 1b: posts/index.html, projects/index.html used if you run new on a subdirectory {#project-tree-ref-3}
##### ref 4:  {#project-tree-ref-4}
##### ref 5:  {#project-tree-ref-5}
##### ref 6:  {#project-tree-ref-6}
##### ref 7:  {#project-tree-ref-7}
##### ref 8:  {#project-tree-ref-8}
##### ref 9:  {#project-tree-ref-9}
##### ref 10:  {#project-tree-ref-10}
##### ref 11:  {#project-tree-ref-11}
##### ref 12:  {#project-tree-ref-12}
##### ref 13:  {#project-tree-ref-13}
##### ref 14:  {#project-tree-ref-14}
##### ref 15:  {#project-tree-ref-15}
##### ref 16: separate from the main styles for caching long term on the browser {#project-tree-ref-16}
##### ref 17: pulls from files this folder and from components {#project-tree-ref-17}
##### ref 18:  {#project-tree-ref-18}
##### ref 19:  {#project-tree-ref-19}
##### ref 20:  {#project-tree-ref-20}
##### ref 21:  {#project-tree-ref-21}
##### ref 22:  {#project-tree-ref-22}
##### ref 23:  {#project-tree-ref-23}
##### ref 24: only http code 404 comes with a template in hugo. For other common codes, static pages have been made that will be placed in root once the site is generated. Then the `.htaccess` from the roots static will have definitions for those custom code pages. {#project-tree-ref-24}
##### ref 25:  {#project-tree-ref-25}
##### ref 26:  {#project-tree-ref-26}
##### ref 27:  {#project-tree-ref-27}

### pagination

### posts & projects

### shortcodes

### all the hacky shit

## scss

### visual style


### highlights and hacks

#### the halftone plate

The 'halftone' dot pattern used in the background is actually a tiled vector drawing on top of the background-image.

```xml
<svg id="halftone-plate" width="0" height="0">
	<defs>
		<pattern id="halftone" patternUnits="userSpaceOnUse" x="0" y="0" width="4" height="4" viewBox="0 0 4 4">
			<rect width="1" height="3" x="1" y="0" fill="rgba(0,0,0,0.15)"></rect>
			<rect width="3" height="1" x="0" y="1" fill="rgba(0,0,0,0.15)"></rect>
			<rect width="1" height="1" x="1" y="1" fill="rgba(0,0,0,0.4)" stroke="rgba(0,0,0,0.05)" stroke-width="2"></rect>
		</pattern>
	</defs>
	<g>
		<rect x="0" y="0" width="100%" height="100%" fill="url(#halftone)"></rect>
	</g>
</svg>
```

{{< img src="halftone-plate-sample-532.png" class="full" >}}

This looks pretty good! *however*, there's *one* trade off to this method.
And it's also the reason it works so well. `<rect x="0" y="0" width="100%" height="100%" ...`
will render a plate the size of the viewport. so while theres no overdraw, the plate also *does not move*

{{< vid src="halftone-showcase.webm" loop="true" >}}

SEE ^^^ NOT MOVING!  
Pretty yucky if you can notice it. Fortunately, youd only see the problem if you have a highdpi display ***and*** are looking for it

## a call to the old ways

### personality

#### badges

### personal blogs in general

#### examples

##### neocities

##### underground webrings, i see u

## whats the point of it all




fa gg dsa g asd g adgs a a a a a a a a a a a a a a a a a a a aa a a a a a a a a a a a a  a
fa gg dsa g asd g adgs a a a a a a a a a a a a a a a a a a a aa a a a a a a a a a a a a  a

fa gg dsa g asd g adgs a a a a a a a a a a a a a a a a a a a aa a a a a a a a a a a a a  a
fa gg dsa g asd g adgs a a a a a a a a a a a a a a a a a a a aa a a a a a a a a a a a a  a
fa gg dsa g asd g adgs a a a a a a a a a a a a a a a a a a a aa a a a a a a a a a a a a  a
fa gg dsa g asd g adgs a a a a a a a a a a a a a a a a a a a aa a a a a a a a a a a a a  a
fa gg dsa g asd g adgs a a a a a a a a a a a a a a a a a a a aa a a a a a a a a a a a a  a
fa gg dsa g asd g adgs a a a a a a a a a a a a a a a a a a a aa a a a a a a a a a a a a  a
fa gg dsa g asd g adgs a a a a a a a a a a a a a a a a a a a aa a a a a a a a a a a a a  a
fa gg dsa g asd g adgs a a a a a a a a a a a a a a a a a a a aa a a a a a a a a a a a a  a
fa gg dsa g asd g adgs a a a a a a a a a a a a a a a a a a a aa a a a a a a a a a a a a  a
fa gg dsa g asd g adgs a a a a a a a a a a a a a a a a a a a aa a a a a a a a a a a a a  a


