---
title: 'Sundry Saturdays: Getting the Real Word Count'
author: Joseph Louthan
type: post
publishDate: 2020-06-27
url: /sundry_saturday/2020-06-27-sundry_saturday/
categories:
  - Links
tags:
  - 'Sundry Saturday'
draft: false
---
## I Write Some
And now I am curious abut the amount of of the words I write per week *concerning* my blog only.

I got the idea from the weekly Grammarly stats:

![grammarly_stats](../../images/grammarly_stats.jpeg)

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
```bash
$ crontab -l
0 9 * * 1	~/bin/word_count
```

Notes:
`awk '{ print $1 }'` - Without this pipe, too much whitespace

`words_written=$(($this_word_count-$previous_word_count))` - This is the new bash POSIX way of doing calculations

`echo -e "$date \t$previous_word_count \t$this_word_count \t$words_written" >> $output_file` - -e is necessary for \t whereas \t is for tab

------

## P.S.

Since I did not have that many months working in Hugo, I decided to a word count since the beginning of the project:
```bash
days=( 144 137 130 123 116 109 102 95 88 81 74 67 60 53 46 39 32 25 18 11 )
for i in "${days[@]}"; do
  echo "$(find $content -name '*.md' -mtime +"$i" -type f -exec awk 1 {} + | wc -w | awk '{ print $1 }')"
done
```
(Yes, very messy I know.)



To produce this:
```bash
Week Of     Last    Current Written
2020-04-13	        Start   177780
2020-04-20	177780	221095	43315
2020-04-27	221095	224295	3200
2020-05-04	224295	224295	0
2020-05-11	224295	227031	2736
2020-05-18	227031	231445	4414
2020-05-25	231445	233508	2063
2020-06-01	233508	273059	39551
2020-06-08	273059	277971	4912
2020-06-15	277971	286995	9024
2020-06-22	286995	305863	18868
```

This is very encouraging to see!

## P.P.S

![img](../../images/latest.jpeg)

```bash
jlouthan@ironhide > ~/bin >> master > cat theologicus_word_count
Week Of		Last    Current Written
2020-04-13	       Starting 177780
2020-04-20	177780	221095	43315
2020-04-27	221095	224295	3200
2020-05-04	224295	224295	0
2020-05-11	224295	227031	2736
2020-05-18	227031	231445	4414
2020-05-25	231445	233508	2063
2020-06-01	233508	273059	39551
2020-06-08	273059	277971	4912
2020-06-15	277971	286995	9024
2020-06-22	286995	305863	18868
2020-06-29 	314930 	378783 	63853
```

MONSTEROUS!