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

# Heading GeblgmqwPy 1
## Heading GeblgmqwPy 2
### Heading GeblgmqwPy 3
#### Heading GeblgmqwPy 4
##### Heading GeblgmqwPy 5
###### Heading GeblgmqwPy 6

## hugo structure

### overview

Here is the hugo project structure.

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
##### ref 3:  {#project-tree-ref-3}
##### ref 4:  {#project-tree-ref-4}
##### ref 4a:  {#project-tree-ref-4a}
##### ref 4b:  {#project-tree-ref-4b}
##### ref 4c:  {#project-tree-ref-4c}
##### ref 5:  {#project-tree-ref-5}
##### ref 6:  {#project-tree-ref-6}
##### ref 6a:  {#project-tree-ref-6a}
##### ref 7:  {#project-tree-ref-7}
##### ref 8:  {#project-tree-ref-8}
##### ref 9:  {#project-tree-ref-9}
##### ref 10:  {#project-tree-ref-10}
##### ref 11a: separate from the main styles for caching long term on the browser {#project-tree-ref-11a}
##### ref 11b: pulls from files this folder and from components {#project-tree-ref-11b}
##### ref 12:  {#project-tree-ref-12}
##### ref 13a:  {#project-tree-ref-13a}
##### ref 13b:  {#project-tree-ref-13b}
##### ref 13c:  {#project-tree-ref-13c}
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


