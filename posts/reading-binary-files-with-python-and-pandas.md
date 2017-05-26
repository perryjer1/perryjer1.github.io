<!-- 
.. title: Reading binary files with Python and Pandas
.. slug: reading-binary-files-with-python-and-pandas
.. date: 2017-05-26 15:10:36 UTC-05:00
.. tags: python
.. category: 
.. link: 
.. description: 
.. type: text
-->

We use a lot of binary files at work for market data. There are pros
and cons that I don't want to argue about here but I'd like to focus
on a nice feature in pandas for loading binary data. And actually, it
is a numpy feature but I end up with a DataFrame so I think of it as
pandas.

<!-- TEASER_END -->

When reading binary files in python before, I would do something like
this:

```python
import struct

with open(filename, "rb") as infile:
	# read e.g. open/high/low/close data
	op = struct.unpack("d", infile.read(8))[0]
	hi = struct.unpack("d", infile.read(8))[0]
	lo = struct.unpack("d", infile.read(8))[0]
	cl = struct.unpack("d", infile.read(8))[0]
```

That of course is grossly oversimplified but you get the point. And
you put that in a loop and read all the values that are actually in
the file and lo and behold it was the morning and the evening of the
second day and it was slow.

Turns out that pandas, er, numpy, has a very efficient way to read
binary files that are laid out as sequences of records like ours. So
now I do this:

```python
import numpy as np
import pandas as pd

dt = np.dtype([("open", np.float64),
               ("high", np.float64),
			   ("low", np.float64),
			   ("close", np.float64)])
with open(filename, "rb") as infile:
	data = np.fromfile(infile, dtype=dt)
df = pd.DataFrame.from_records(data)
```

And lo and behold it was the morning and the evening of the third day
and it was fast. And good.
