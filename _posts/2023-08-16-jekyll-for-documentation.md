---
layout: post
title: Using Jekyll for Documentation
date: 2023-08-16 08:00:00 +0800
description: >
  Thig blog describes the Jekyll features that I find useful for generating
  maintainable technical documentation.
img: jekyll-for-documentation.png
img-alt: Image from pngtree.com # Add image post (optional)
tags: [Documentation, Software] # add tag
---

When our technical documentation software subscription was expiring, I was
quite hesitant about renewing it as the fee was quite pricey, so I set about
looking for a free and/or open source alternative.

## The Winner - Jekyll

After evaluating several options - including Adobe Framemaker, Hugo,
Docusaurus, and Asciidoctor - I finally landed on the static site generator,
{{ site.data.external-links.jekyll_ssg }}.

## Why I Chose Jekyll

To help with my decision, I evaluated different documentation tools and
decided on Jekyll based on the factors below.

_Note: Other factors that were also considered - but did not strongly impact my
decision - include built-in search engine optimization (SEO) capabilities,
automatic table of contents (TOC), support on different operating systems,
localization features, and software support (e.g. documentation for the
tool)._

### Cost

This is the obvious factor that triggered the search for an alternative
documentation tool to begin with.
Since Jekyll is a free and open source tool, this encouraged me to look more
closely at the features available in Jekyll.

### Support for shared and reusable content

One of the best things about Jekyll is the support for shared and reusable
content through the use of {{ site.data.external-links.jekyll_variables }} and
the {{ site.data.external-links.jekyll_include }}.

Variables can be defined globally (for the site) in data files, or locally
(per page) using Front Matter. This makes documentation maintenance a lot
easier as any changes made in a single source file / location will be
automatically reflected in all references to that variable through out the
site.

Besides that, `include` tags enable shared content to be customizable based on
the (optional) parameters passed to the `include` file.

### Liquid templating language

I absolutely love the {{ site.data.external-links.jekyll_liquid }} and it is
one of the main reasons I decided to use Jekyll for documentation.

Besides the common Liquid tags and filters that are described in the Jekyll
website, I have found control flow tags (e.g. `if...endif`,
`unless...endunless`, `case...when`, etc...), iteration tags (e.g.
`for...endfor`, `limit`...`offset`), and other liquid operators and filters
(e.g. `!=`, `assign`, `capture...endcapture`, `split`, etc...) to be
extremely useful when writing technical documentation.

For example, I use a combination of Liquid tags and operators (with the help
of some CSS) to evenly split and print a list of values into a 2-column layout.

```{% raw %}
{% capture list %}Windows Vista,Windows 7,Windows 8,Windows 8.1,
Windows Server 2012 R2,Windows 10, Windows Server 2016,Windows Server 2019,
Windows 11{% endcapture %}

{% assign listarr = list | split: "," %}
{% assign firsthalf = listarr.size | divided_by: 2.0 | ceil %}

<div class="content-row">
  <div class="content-two-column-left">
    <ul>
      {% for item in listarr limit:firsthalf %}
        <li>{{ item }}</li>
      {% endfor %}
    </ul>
  </div>
  <div class="content-two-column-right">
    <ul>
      {% for item in listarr offset:firsthalf %}
        <li>{{ item }}</li>
      {% endfor %}
    </ul>
  </div>
</div>{% endraw %}
```

The sample code above will generate the following output:

{% capture list %}Windows Vista,Windows 7,Windows 8,Windows 8.1,
Windows Server 2012 R2,Windows 10, Windows Server 2016,Windows Server 2019,
Windows 11{% endcapture %}

{% assign listarr = list | split: "," %}
{% assign firsthalf = listarr.size | divided_by: 2.0 | ceil %}

<div class="content-row">
  <div class="content-two-column-left">
    <ul>
      {% for item in listarr limit:firsthalf %}
        <li>{{ item }}</li>
      {% endfor %}
    </ul>
  </div>
  <div class="content-two-column-right">
    <ul>
      {% for item in listarr offset:firsthalf %}
        <li>{{ item }}</li>
      {% endfor %}
    </ul>
  </div>
</div>

### Ease of use

One important criteria was that new team members should not have to spend too
much time learning how to use the technical documentation software.
I found the Jekyll installation and build steps to be relatively
straightforward.
It also did not take me too long to understand the Jekyll files and directory
structure, which made it simple enough to build my site on top of any selected
Jekyll theme.

### Compatibility with version control systems (VCS)

I preferred text-based source files that would work well with VCS.
Jekyll happened to be perfect in this aspect as content was mainly written in
Markdown, Liquid, and HTML.

### Customization

Jekyll\'s layout files lets you define multiple page templates that can be used
for different content types in your site.

There are also many free Jekyll themes available which could be used as a base
template for my documentation site.

## What was missing from Jekyll

### Multiple output formats

While HTML was the main output format, we did get requests from time to time
for the PDF version of our software documentation, so this was taken into
consideration when evaluating Jekyll.

While there are plugins available, there is no quick and easy way to generate a
single PDF for the whole documentation site, so we resorted to using the
{{ site.data.external-links.wkhtmltopdf }} tool to render our HTML content
into PDF.

## Conclusion

Despite the lack of support for multiple output formats, Jekyll turned out to
be a good choice as a technical documentation tool. I decided on using Jekyll
almost five years ago, and have not regretted my decision.

What do you think?
What other alternative documentation software do you know of that are
comparable with Jekyll?

