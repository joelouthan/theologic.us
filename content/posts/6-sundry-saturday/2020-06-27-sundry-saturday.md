---
title: 'Sundry Saturdays: Getting the Real Word Count'
author: Joseph Louthan
type: post
publishDate: 2020-06-27
url: /sundry-saturday/2020-06-27-sundry-saturday/
categories:
  - Links
tags:
  - 'Sundry Saturday'
draft: false
---
## I Write Some
And now I am curious abut the amount of of the words I write per week *concerning* my blog only.

I got the idea from the weekly Grammarly stats:

/grammarly_stats.jpeg

... which mentions only the words I have checked by Grammarly which does include only Romans from the blog plus email, comments, tweets. I want Romans *and* the rest of the blog. I really don't care about the other stuff.

Enter in the command **wc**
```bash
$ wc -c next-10-0-weeks-posts
265 next-10-0-weeks-posts
```

But you see all of that whitespace? That is no bueno for calculations.

I wrote a script:
```bash
#! /bin/bash
# date command: MACOS

bin=$HOME/bin/
content=/Users/jlouthan/Sites/theologic.us/content/posts
output_file=$bin/theologicus_word_count
date=$(date -j +%F)
previous_word_count=$(find $content -name '*.md' -mtime +7 -type f -exec awk 1 {} + | wc -w | awk '{ print $1 }')
this_word_count=$(find $content -name '*.md' -type f -exec awk 1 {} + | wc -w | awk '{ print $1 }')
words_written=$(($this_word_count-$previous_word_count))

echo -e "$date \t$previous_word_count \t$this_word_count \t$words_written" >> $output_file
```

And then run ~/bin/word_count script every Monday at 10AM:
```cmd
$ crontab -l
0 9 * * 1	~/bin/word_count
```

Notes:
1. `awk '{ print $1 }'` - Without this pipe, too much whitespace
2. `words_written=$(($this_word_count-$previous_word_count))` - This is the new bash POSIX way of doing calculations
3. `echo -e "$date \t$previous_word_count \t$this_word_count \t$words_written" >> $output_file` - -e is necessary for \t whereas \t is for tab

------

