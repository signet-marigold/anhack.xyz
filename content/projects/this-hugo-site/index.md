---
title: "This Hugo Site"
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

## Intro

Alright so first off I wanted a static site gen and I was looking at the options available.
[Jekyll](https://jekyllrb.com/) honestly is fine I have no real problems with It but it doesn't appear to have the functionality I need. and [Eleventy](https://www.11ty.dev/) (actually a cool project) but not exactly what I was looking for.
[Hugo](https://gohugo.io/)s modularity and live-reload is amazing, plus it's designed to be a general purpose generator. Meaning theres very little in the way of doing anything I want 

### Overview

## Hugo

### Hugo Stucture

Here is the project structure.


```render
Project Root
.
├── archetypes{{< footnote title="1" target="project-tree-ref-1" >}}
│   ├── default.md{{< footnote title="1a" target="project-tree-ref-1b" >}}
│   ├── posts{{< footnote title="1b" target="project-tree-ref-1c" >}}
│   └── projects
├── assets{{< footnote title="2" target="project-tree-ref-2" >}}
│   └── images
├── config.toml{{< footnote title="3" target="project-tree-ref-3" >}}
├── content{{< footnote title="4" target="project-tree-ref-4" >}}
│   ├── _index.md{{< footnote title="4a" target="project-tree-ref-4a" >}}
│   ├── posts{{< footnote title="4b" target="project-tree-ref-4b" >}}
│   └── projects{{< footnote title="4c" target="project-tree-ref-4c" >}}
├── deploy{{< footnote title="5" target="project-tree-ref-5" >}}
├── layouts{{< footnote title="6" target="project-tree-ref-6" >}}
│   ├── index.html
│   ├── partials{{< footnote title="6a" target="project-tree-ref-6a" >}}
│   └── robots.txt
├── static{{< footnote title="7" target="project-tree-ref-7" >}}
│   ├── badges
│   ├── icons
│   └── img
└── themes{{< footnote title="8" target="project-tree-ref-8" >}}
    └── asperity
        ├── archetypes
        ├── assets
        │   ├── css
        │   ├── js
        │   └── scss
        │       ├── components{{< footnote title="9" target="project-tree-ref-9" >}}
        │       ├── css
        │       │   └── normalize.css{{< footnote title="10" target="project-tree-ref-10" >}}
        │       ├── fonts
        │       │   ├── noto-sans
        │       │   │   └── <font parts>
        │       │   └── _noto-sans.scss (font collection)
        │       ├── _*.scss
        │       ├── fonts.scss{{< footnote title="11a" target="project-tree-ref-11a" >}}
        │       └── main.scss{{< footnote title="11b" target="project-tree-ref-11b" >}}
        ├── i18n{{< footnote title="12" target="project-tree-ref-12" >}}
        ├── layouts
        │   ├── _default{{< footnote title="13a" target="project-tree-ref-13a" >}}
        │   ├── partials{{< footnote title="13b" target="project-tree-ref-13b" >}}
        │   └── shortcodes{{< footnote title="13c" target="project-tree-ref-13c" >}}
        ├── static
        │   ├── 40{x}.html{{< footnote title="14" target="project-tree-ref-14" >}}
        │   ├── css
        │   ├── fonts
        │   ├── icons
        │   └── img
        ├── config.toml
        └── theme.toml
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
##### ref 1a: Used if you run new on a main directory (e.g. new posts/new-post.md) {#project-tree-ref-1a}
##### ref 1b: posts/index.html, projects/index.html used if you run new on a subdirectory {#project-tree-ref-1b}
##### ref 2: Assets are resources that are transformed in some way by hugo before they are used {#project-tree-ref-2}
##### ref 3: config here will override any variables set by configs in the theme folder {#project-tree-ref-3}
##### ref 4: content. where all of the posts, projects and any other page markdown lives {#project-tree-ref-4}
##### ref 4a: is the homepage of the site {#project-tree-ref-4a}
##### ref 4b: markdown here will live on the /posts/ folder after generation {#project-tree-ref-4b}
##### ref 4c: markdown here will live on the /projects/ folder after generation {#project-tree-ref-4c}
##### ref 5: is a script I made for generating and then sending the ready site to my host server {#project-tree-ref-5}
##### ref 6: most layouts are defined in the theme however there are a few that are site specific {#project-tree-ref-6}
##### ref 6a: like the badges in the footer for example {#project-tree-ref-6a}
##### ref 7: resources that don't need to be transformed. as they appear in this folder they will be in the root {#project-tree-ref-7}
##### ref 8: if not already defined, every file in the theme will be used to generate the site {#project-tree-ref-8}
##### ref 9: i've separated the css into different parts when it felt like they could be grouped {#project-tree-ref-9}
##### ref 10: some browsers treat default styles slightly differently. this fixes the largest offenders {#project-tree-ref-10}
##### ref 11a: separate from the main styles for caching long term on the browser {#project-tree-ref-11a}
##### ref 11b: pulls from files this folder and from components {#project-tree-ref-11b}
##### ref 12: language translations. some strings show up as a part of the base layout. not like a have multi language support rn tho {#project-tree-ref-12}
##### ref 13a: defines layoutes for basic page types {#project-tree-ref-13a}
##### ref 13b: parts of a layout so they can be reused {#project-tree-ref-13b}
##### ref 13c: shortcodes are almost like partials except they are suposed to only be used inside of markdown files in the \{\{\< shortcodename \>\}\} format {#project-tree-ref-13c}
##### ref 14: only the 404 page comes with a template in hugo. For other common codes, static pages have been made that will be placed in root once the site is generated. Then the `.htaccess` from the roots static will have definitions for those custom code pages. {#project-tree-ref-14}

### pagination

### posts & projects

### shortcodes

### all the hacky shit

#### image processing and DOM manipulation

This piece of shite gets me an image object from a link. Whether it's a external url, global resource or just local to the post dir; this really shouldn't break
```go
{{ $image := "" }}
// If it looks like an external link
{{ if findRE "(^(https?:)?//)" (lower $imageLink) }}
	{{ with resources.GetRemote $imageLink }}
		{{ with .Err }}
			{{ errorf "%s" . }}
		{{ else -}}
			{{ $image = . }}
		{{ end }}
	{{ else }}
		{{ errorf "Unable to get remote resource %q in %s" $imageLink .Page }}
	{{ end }}
{{ else -}}
	// Look for file in global resources
	{{ with resources.Get $imageLink }}
		{{ with .Err }}
			{{ errorf "%s" . }}
		{{ else -}}
			{{ $image = . }}
		{{ end }}
	{{ else }}
		// Look for file in page resources
		{{ with $.Page.Resources.GetMatch $imageLink -}}
			{{ with .Err }}
				{{ errorf "%s" . }}
			{{ else }}
				{{ $image = . }}
			{{ end }}
		{{ else }}
			{{ errorf "Unable to get local resource %q in %s" $imageLink .Page }}
		{{ end }}
	{{ end }}
{{ end -}}
```

Find greatest common factor:
this reduces the image dimentions into the smallest integer ratio *(assuming it takes fewer than a thousand iterations)*
```go
// Find greatest common factor
{{ $n1 := $image.Width }}
{{ $n2 := $image.Height }}
{{ range seq 1000 }}
	{{ if eq $n1 $n2 }}
		{{ break }}
	{{ end }}
	{{ if gt $n1 $n2 }}
		{{ $n1 = sub $n1 $n2 }}
	{{ else }}
		{{ $n2 = sub $n2 $n1 }}
	{{ end }}
{{ end }}

// Simplified ratio
{{ $dHorizontal := div $image.Width $n1 }}
{{ $dVertical   := div $image.Height $n1 }}
```

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
Pretty yucky if you can notice it. Fortunately, you'd only see the problem if you have a highdpi display ***and*** are looking for it



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


