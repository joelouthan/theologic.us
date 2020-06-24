---
title: 'Sundry Saturdays: Cupper Theme on Hugo, Prism Syntax Highlighting & You'
author: Joseph Louthan
type: post
publishDate: 2020-07-04
url: /sundry-saturday/2020-07-04-sundry-saturday/
categories:
  - Links
tags:
  - 'Sundry Saturday'
draft: false
---
## Why Did My Code Blocks Didn't Work?
I will spare you the details but everything time I attempted to do Syntax Highlighting (i.e. fancying color coding of code based on the language you choose), I would end up getting black on super dark grey.

Wholly unreadable.

I do have cupper theme forked so I thought I was missing something. I reached out to the author. To which he replied, "[it ain't my fault](https://github.com/zwbetz-gh/cupper-hugo-theme/issues/38)." Also, [RTFM](https://cupper-hugo-theme.netlify.app/cupper-shortcodes/#syntax-highlightin).

<iframe width="560" height="315" src="https://www.youtube.com/embed/rhFjc5dcKQI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Fair enough.

If you are using the Cupper theme right out the box, the ability to use [Prism](https://prismjs.com/) *works* but the code syntaxes are slim pickings.

You have to go to Prism's website and customize it.

Here's how.

1.  Go to [Prism's Download page](https://prismjs.com/download.html#themes=prism-tomorrow&languages=markup+css+clike+javascript)

2. Pick and choose your options including theme and languages and some add-ons.
3. Download the .js file and insert into theme/cupper/static/js/ directory
4. Download the .css file and insert into theme/cupper/static/css/ directory
5. You will most certainly have to stop and start your Hugo server
6. Profit$