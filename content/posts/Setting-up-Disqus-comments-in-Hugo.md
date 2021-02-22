---
title: "Setting Up Disqus Comments in Hugo"
date: 2021-01-03T16:50:07+01:00
tags: ["Hugo","PaperMod","Disqus","Installation"]
featured_image: ""
description: "This guide applies to Hugo themes, such as the PaperMod theme. Depending on your Hugo theme, setting up Disqus or other comment services can differ but it will be very similar to this."
draft: false
---

## Create comments file
First create a html file in:
`layouts/partials/comments.html`
This is applicable mostly for the PaperMod theme. Other themes usually use a disqus.html file. It is important to name the file in the right way so your theme will recognise it. Check the documentation of your theme, in my case the PaperMod theme documentation about comments is here: https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-features/#comments


## Hugo Disqus template
Copy from Hugo repository [tpl/tplimpl/embedded/templates/disqus.html](https://github.com/gohugoio/hugo/blob/edc5c4741caaee36ba4d42b5947c195a3e02e6aa/tpl/tplimpl/embedded/templates/disqus.html)

Add all the lines in the previously created `comments.html` file

I replaced the lines:
{{< highlight html >}}
{{with .Params.disqus_identifier }}this.page.identifier = '{{ . }}';{{end}}
{{with .Params.disqus_title }}this.page.title = '{{ . }}';{{end}}
{{with .Params.disqus_url }}this.page.url = '{{ . | html  }}';{{end}}
{{< /highlight >}}

With these:
{{< highlight html >}}
this.page.url = '{{ .Permalink }}';
this.page.identifier = '{{ .Permalink }}';
this.page.title = '{{ .Title }}';
{{< /highlight >}}

---
