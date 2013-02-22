Count-Min Sketch
================

Count-Min Sketch is a probabilistic sub-linear space streaming algorithm
 which can be used to summarize a data stream in different ways. It's 
mostly used to find **Heavy Hiiters** in a data set. This data structure
is pretty recent. It was introduced in 2003. Sine then, it has inspired
many applications, extensions, and variations.

This probabilistic data structure was first proposed by Muthukrishnan
and Cormode (see references below for more details).

Count-Min Sketch Internals
--------------------------

The data structure primarily consists of a fixed array of counters, of 
width *w* and depth *d*. Every entry is called a counter.
 The counters are all initialized to zeros.
Each row of counters is associated with a different hash function (out
of k-pairwise independent hash functions). The hash function maps items
uniformly onto the range {1,2,...,w}. The hash functions do not need to be 
particularly strong or as complex as cryptographic hash functions. So you
can just use a linear hash. But is important that the hash function 
for each row be distinct (and pairwise indepenent!).

There are two main operations: UPDATE(i,c), ESTIMATE(i). UPDATE(i,c)
updates (incremenets) the count associated with the item *i*. On the other 
hand, ESTIMATE(i) returns an estimate of the count associated with an 
item *i*.

For more details on the data structure internals, see the summary in this
repository.

Using the Program
-----------------

You can create a new Count-Min skectch like this:

    CountMinSketch c(0.1, 0.01);

The signature of the constructor is
 `ContMinSketch(float eps, float gamma)`
where `0.01 < eps < 1` is the possible error to allow and
`0 < gamma < 1` is the probability that the possible error
to occur. The smaller these values the more accurate are
the estimates of the Count-Min sketch but the more space
would be used in estimations.

To update the count of an item in the Count-Min sketch, use
`c.update(item, int count)` where item is either a string
constant or an integer. For example,

	 c.update("heylo", 1);
	 c.update(20, 2);
	 c.update("heylo", 1);

To estimate the total count of a specific item, use
`c.estimate(item)` where item is either a string constant
or an integer. For example,
   
   c.estimate(20);
   c.esimate("hello");
   c.estimate("heylo");
   // returns 2,0,2 respectively

To retrieve the total count of all the items in the data
structure, use `c.totalcount()`.

References
----------
* [Count-Min Sketch and its Applications](https://sites.google.com/site/countminsketch)

* [Count-Min Sketch on Wikipedia] (https://en.wikipedia.org/wiki/Count-Min_sketch)

* [Approximating Data with the Count-Min Data Structure] (http://dimacs.rutgers.edu/graham/pubs/papers/cmsoft.pdf)

* [An improved Data Stream Summary: the Count-Min Sketch and its Applications] (http://www.research.att.com/people/Cormode.Graham/library/publicationsCormodeMuthukrishnan)

MIT Open Source License
-----------------------

Copyright © 2012 Daniel Alabi

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.