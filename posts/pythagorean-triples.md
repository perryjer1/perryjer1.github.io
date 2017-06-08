<!-- 
.. title: Pythagorean triples
.. slug: pythagorean-triples
.. date: 2017-06-08 09:54:40 UTC-05:00
.. tags: mathjax
.. category: 
.. link: 
.. description: 
.. type: text
-->

I was looking for a way to generate Pythagorean triples and figured
there had to be some sort of formula or algorithm. And of course there
is but I did not expect to see one from Euclid. Euclid! What else did
that guy do? It is always humbling to learn something from someone
that lived over two thousand years ago.

<!-- TEASER_END -->

The formula is pretty straightforward:

$$ a = m^2 - n^2 $$
$$ b = 2mn $$
$$ c = m^2 + n^2 $$

To verify that is a Pythagorean triple is just a matter of expanding

$$ a^2+b^2 = (m^2-n^2)^2 + (2mn)^2 $$

to show that it is equal to

$$ (m^2 + n^2)^2 = c^2 $$

There are some important details, restrictions on `n` and `m` like

$$ m > n > 0 $$

and `n` and `m` should be coprime for best results (getting primitive
triples). Read up on it [here](https://en.wikipedia.org/wiki/Pythagorean_Triple).

In retrospect, it makes sense that Euclid would know this. He knew a
thing or two about geometry.
