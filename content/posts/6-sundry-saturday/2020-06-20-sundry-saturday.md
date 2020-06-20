---
title: 'Sundry Saturdays: Articles on Hugo'
author: Joseph Louthan
type: post
publishDate: 2020-06-20
url: /sundry-saturday/2020-06-20-sundry-saturday/
categories:
  - Links
tags:
  - 'Sundry Saturday'
draft: false
---

## Times, they are a changin'

So taking a break from social media which, in turn, leaves Friday and Saturday's posts a bit dry.

I don't know what I am going to do for Fridays. But Saturdays, I will do more technical posts on things like migrating from Wordpress to Hugo, messing around with themes and the like.

------

## Google fonts in Hugo

Playing around with Google Fonts in Hugo:

<img src="../../images/image-20200619192818033.png" alt="image-20200619192818033" style="zoom:50%;" />

... based on this snippet:

https://gist.github.com/jeremybise/a6afea2d4c7f9044180ffeb663a617cf

Here's how I did it. (These are straight from my site)

1. Find your head.html (mine was in *webroot*/themes/*theme-name*/layouts/partials) and add this snippet

   ```html
   <head>
   {{ partial "google-fonts" . }}
   </head>
   ```

   Anywhere is good as long as it's not within a meta tag
   
2. Stick this into your config.toml

   ```toml
   [params]
   google_fonts = [
     ["Cinzel", "100, 200, 300, 400, 500, 600, 700, 800, 900"]
   ]
   ```
100-900 are the various weights--100 being the thinnest and 900 being the boldest.

3. Go back into *webroot*/themes/*theme-name*/layouts/partials and add google-fonts.html:
   ```html
   {{ if .Site.Params.google_fonts }}
     {{ $fonts := slice }}
     {{ range .Site.Params.google_fonts }}
       {{ $family := replace (index (.)  0) " " "+" }}
       {{ $weights := replace (index (.) 1) " " "" }}
       {{ $string := print $family ":" $weights }}
       {{ $fonts = $fonts | append $string }}
     {{ end }}
     {{ $url_part := (delimit $fonts "|") | safeHTMLAttr }}
     <link {{ printf "href=\"//fonts.googleapis.com/css?family=%s\"" $url_part | safeHTMLAttr }} rel="stylesheet">
   {{ else}}
     <!-- specify a default in case custom config not present -->
     <link href="//fonts.googleapis.com/css?family=Roboto:300,400,700" rel="stylesheet">
   {{ end }}
   ```

4. Finally, find your css and edit appropriately. So the site Description I wanted to alter was under library-desc. So:
   ```css
   .library-desc {
       font-size: 0.60rem;
       font-weight: 100;
       font-family: "Cinzel", Times, serif;
       margin-top: 0.5rem;
       margin-left: auto;
       margin-right: auto;
       max-width: 25rem;
   }
   ```

5. If you are running Hugo with the default NoFastRender, it *should* refresh the page automatically--give or take about 10 seconds.

Play around with it and see if that works for you.