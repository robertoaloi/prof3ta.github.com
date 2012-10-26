--- 
layout: post
title: "The v(N) function in Erlang"
date: 2009-02-20 00:00
categories: [erlang, shell, productivity]
published: false
---
The Erlang shell offers many helper functions, which allow you to
interact with the commands history. A useful function is
<code>v(Number)</code>, which returns the computed value for the
_N_-th expression in the shell history.

See the following usage example:

<pre>
Eshell V5.6.5  (abort with ^G)
1&gt; 2 * 2.
4
2&gt; v(1).
4
3&gt; 
</pre>

You can get the whole list of helper functions by opening an Erlang
shell and by typing:

<pre>
help().
</pre>
