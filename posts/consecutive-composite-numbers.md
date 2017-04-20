<!-- 
.. title: Consecutive Composite Numbers
.. slug: consecutive-composite-numbers
.. date: 2017-04-20 12:57:07 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

I recently read that there exist strings of consecutive composite
numbers of arbitrary length. That hurts my head, just a little. So
even though there are infinitely many prime numbers, the gaps between
them can be arbitrarily long.

To generate a sequence of `n` numbers that are composite, take
`(n+1)! + 2`, `(n+1)! + 3`, ..., up to `(n+1)! + n+1`. That has `n`
numbers in it and each is composite: the first is divisible by 2, the
second is divisible by 3, etc.
