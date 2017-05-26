<!-- 
.. title: R tip: dev.off()
.. slug: r-tip-devoff
.. date: 2017-05-19 08:13:44 UTC-05:00
.. tags: R
.. category: 
.. link: 
.. description: 
.. type: text
-->

When plotting in R and changing parameters via `par`, I have been very
careful about saving and restoring them:

```R
old <- par()
par(mar = c(7.1, 4.1, 4.1, 2.1))
## plot something, then restore:
par(old)
```

If you do that as is, you will get several warnings when you call
`par(old)` about parameters that cannot be set. The way around that is
to pass the `no.readonly` flag:

```R
old <- par(no.readonly = TRUE)
## ...
par(old)
```

If you are like me, you always call it the first way until you get the
warnings, then call it the second way and you get annoyed that you
have to type All That Extra Stuff.

One thing I learned this week is `par` returns a list of the old
parameters that you are setting. So for example,

```R
old <- par(mar = c(7.1, 4.1, 4.1, 2.1))
```

`old` now only has one element named `mar` which has the old value in
it. Calling

```R
par(old)
```

now only resets that one value that was changed.

I've always thought the `par` function changed parameters per session.
The second thing I learned this week is the `par` function sets
parameters per device. That's not exactly a secret; the first line of
the Details section when you `?par` says

> Each device has its own set of graphical parameters.

That means that to drop all parameter changes and go back to the
defaults, we can just call e.g.

```R
dev.new()
```

or even `dev.off()`. No need to capture and restore anything.
