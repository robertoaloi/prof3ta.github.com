--- 
layout: post
title: "Tracing Erlang Functions"
date: 2009-02-23 00:00
categories: [debug, erlang, trace] 
---
Tracing Erlang functions for debugging purposes is probably simpler
than you could even imagine. Let's say you wrote the module below and
that you want to know what happens when you call one of its functions.

<pre>
-module(math).
-export([sum/2, diff/2]).

sum(A, B) -&gt;
  A + B.
diff(A, B) -&gt;
  A - B.
</pre>

First of all, compile the module and verify that everything works as
expected:

<pre>
&gt; c(math).
{ok,math}
&gt; math:sum(3,6).
9
</pre>

Now start the tracer wuth the following instruction:

<pre>
&gt; dbg:tracer().
</pre>

You also need to inform the tracer that you want to trace _all_ function
calls performed by _all_ Erlang processes:

<pre>
&gt; dbg:p(all, c).
</pre>

Finally, let the tracer know that you're specifically interested in
the function <code>sum</code>, belonging to the module <code>math</code>:

<pre>
&gt; dbg:tpl(math, sum, x).
</pre>

Please note that <code>x</code> stands for _exception trace_. You're
basically telling the tracer that you want to set a trace which will
show function names, parameters, return values and exceptions thrown
from a given function.

Now that your tracer is activated, try to call the <code>sum/2</code>
function again.

<pre>
&gt; math:sum(3, 6).
</pre>

This time you should see something like the following:

<pre>
(<0.31.0>) call math:sum(3,6)
(<0.31.0>) returned from math:sum/2 -> 9
9
</pre>

To stop the tracer:

<pre>
&gt; dbg:stop().
</pre>

To trace all of the functions belonging to the module <code>math</code>:

<pre>&gt; dbg:tpl(math, x)</pre>

For more information about the Erlang tracing and debugging functionalities, please refer to the official documentation of the <a href="http://erlang.org/doc/man/dbg.html" target="_blank">Erlang <code>dbg</code> module</a>.
