<!-- 
.. title: Reading a UTF-8 csv file from Excel
.. slug: reading-a-utf-8-csv-file-from-excel
.. date: 2017-04-28 08:28:59 UTC-05:00
.. tags: R
.. category: 
.. link: 
.. description: 
.. type: text
-->

I recently upgraded to Windows 10 at work and the latest and greatest
version of Excel. I went to save a csv file to read into R and did not
realize I selected the "UTF-8" option.

<!-- TEASER_END -->

When I read it into R, I saw three strange extra characters in the
first column name. No expert am I in unicode but I know enough to
recognize this was probably a byte-order mark and just needed to be
read differently.

I looked at the arg list for `read.csv` and tried the following:

```R
X <- read.csv(filename, encoding = "utf-8")
```

This seemed very sensible to me since `encoding` is pretty standard
for this sort of thing in e.g. python. It did not work and when I
looked closer, I realized there was another argument, `fileEncoding`:

```R
X <- read.csv(filename, fileEncoding = "utf-8")
```

Oddly, this did not work either. At this point I started mumbling
incoherently.

Naturally, Hadley came to my rescue when I read his answer to [this
StackOverflow question](http://stackoverflow.com/questions/21624796/read-a-utf-8-text-file-with-bom). 
Seems that in R, the correct "encoding" is "utf-8-bom" where bom
stands for byte order mark:

```R
X <- read.csv(filename, fileEncoding = "utf-8-bom")
```

At last. Why do I have to use `fileEncoding` instead of just
`encoding`, and what does the `encoding` variable do anyway? Why do I
have to put "utf-8-bom" instead of just "utf-8"? Why does Excel feel
compelled to put a byte order mark in a UTF-8 file? If I were
industrious and curious, I would find out, but I am lazy and
uninterested so for now it will stay a mystery.
