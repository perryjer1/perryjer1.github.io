<!-- 
.. title: C++ sorting
.. slug: c++-sorting
.. date: 2017-06-20 15:38:38 UTC-05:00
.. tags: c++
.. category: 
.. link: 
.. description: 
.. type: text
-->

I was running some C++ code that was sorting a vector based on a
custom function, something like this:

<!-- TEASER_END -->


```c++
std::sort(vec.begin(), vec.end(), [](const Thing & t1, const Thing & t) {
   ...
})
```

and I was getting the following:

```sh
segmentation fault (core dumped)
```

Gah. Never a good thing to get that. I checked a few things that
seemed related. I checked a few things that did not seem related. I
spent more time on it than I will admit. Finally I
found [this](https://stackoverflow.com/a/1541909) answer on
StackOverflow.

> In C++, your "compare" predicate must be a strict weak ordering. In
> particular, "compare(X,X)" must return "false" for any X.

Turns out that is not a joke, the standard does require a "strict weak
ordering" or else all bets are off. Changing a `<=` to a `<` fixed the
problem. Note to future self: devil, details, etc.
