--- 
layout: post
title: "How they tried to fool tryerlang.org"
date: 2010-10-14 00:00
categories: [erlang, hacking, restrictions, sandbox, tryerlang] 
---

<h2>Preface</h2>

<a title="tryerlang.org" href="http://tryerlang.org" target="_blank">tryerlang.org</a> is an _interactive Erlang Shell_ which allows users to try the power of Erlang directly in a browser, without requiring them to install an Erlang runtime system on their machine. Even if intended for Erlang newbies, tryerlang.org has been subjected to a countless number of attacks conducted by Erlang experts who wanted to circumvent its sandboxing mechanism and to bring down the Erlang node running the application. I must admit that going through the tryerlang.org's logs is being an highly interesting and constructive experience.

In this blog post I will present one of the most elaborated attacks performed on tryerlang.org. The attack, which exploits the Erlang _External Term Representation_, has been performed by a former <a href="http://www.erlang-solutions.com" target="_blank">Erlang Solutions</a>' employee who had access to the tryerlang.org source code. To understand how the attack works, we need to introduce the Erlang _External Term Representation_.

<h2>External Term Representation</h2>

In Distributed Erlang, terms can be transferred from an Erlang node to another one using the so-called _binary_ format. Generic terms are encoded in binary from the sender using the built-in function <code>term_to_binary/1</code> and restored from the receiver using the complementary function <code>binary_to_term/2</code>. A binary message looks like this:

<pre>
<<131,100,0,6,112,105,103,101,111,110>>
</pre>

Which, as you can see, represents the binary encoding of the atom <code>pigeon</code>.

<pre>
1&gt; term_to_binary(pigeon).
&lt;&lt;131,100,0,6,112,105,103,101,111,110&gt;&gt;
2&gt; binary_to_term(&lt;&lt;131,100,0,6,112,105,103,101,111,110&gt;&gt;).
pigeon
</pre>

The _External Term Representation_ of Erlang terms is extensively documented in <a title="Erlang External Term Representation" href="http://www.erlang.org/doc/apps/erts/erl_ext_dist.html" target="_blank">the official Erlang Documentation</a>. Let's see how the attacker used this concept in his own interest.

<h2>Halting the Erlang Node</h2>

To stop the Erlang node running tryerlang.org, the attacker tries at first the following command:

<pre>
&gt; erlang:halt().
</pre>

This function, documented <a title="Erlang Halt" href="http://www.erlang.org/doc/man/erlang.html#halt-0" target="_blank">here</a>, is supposed to _halt_ an Erlang runtime system, indicating a normal exit to the calling environment. The function has been disabled in tryerlang.org for security reasons, so the only result the user get is the following annoying message:

<pre>
"This functionality has been disabled for security reasons in tryerlang.org.".
</pre>

So, the Erlang node is still up and attacker prepares himself a good cup of Swedish coffee. After a couple of minutes playing with the tryerlang.org shell, the attcker notices that tryerlang.org allows you to define custom <a title="Erlang Funs" href="http://www.erlang.org/doc/programming_examples/funs.html" target="_blank">funs</a>. Then, the intuition. A _fun_, as any other Erlang term, <a title="export_ext" href="http://www.erlang.org/doc/apps/erts/erl_ext_dist.html#id83276" target="_blank">can be encoded using the External Terms Representation</a>. The encoded fun could then be executed. This could hopefully fool the sandboxing mechanism protecting the tryerlang.org and could open a world of possibilities to the attacker.

According to the documentation, the external representation of the fun (in the <code>fun M:F/A</code> format) is the following:

<pre>
113 | Module | Function | Arity
</pre>

Where <code>Module</code> and <code>Function</code> are atoms and <code>Arity</code> is an integer.

Atoms themselves can be encoded using the <a title="atom ext" href="http://www.erlang.org/doc/apps/erts/erl_ext_dist.html#ATOM_EXT" target="_blank">ATOM_EXT</a> format:

<pre>
100 | Len | AtomName
</pre>

Where <code>Len</code> is the length of <code>AtomName</code>, expressed using two bytes.

For the atom <code>erlang</code>, which is composed of 6 characters (the letters <code>e</code>, <code>r</code>, <code>l</code>, <code>a</code>, <code>n</code> and <code>g</code>) we obtain:

<pre>
100 | 0, 6 | 101, 114, 108, 97, 110, 103
</pre>

Where the integers in the third section are the ASCII codes for each of the letters composing the word "erlang".

Applying the same reasoning to the atom <code>halt</code>, we obtain:

<pre>
100 | 0, 4 | 104, 97, 108, 116
</pre>

Finally, the arity (an integer) can be encoded using the <a title="small integer ext" href="http://www.erlang.org/doc/apps/erts/erl_ext_dist.html#id80902" target="_blank">SMALL_INTEGER_EXT</a> format:

<pre>
97 | Int
</pre>

So, in our case (arity = 0) we obtain:

<pre>
97 | 0
</pre>

Putting all the pieces together and considering that, in the External Term Representation, the byte <code>131</code> needs to be prepended to the final term, we can encode the <code>erlang:halt/</code>0 function into binary, obtaining:

<pre>
&lt;&lt;131,113,100,0,6,101,114,108,97,110,103,100,0,4,104,97,108,116,97,0&gt;&gt;
</pre>

Let's verify that we didn't do any mistake:

<pre>
&gt; binary_to_term(&lt;&lt;131,113,100,0,6,101,114,108,97,110,103,100,0,4,104,97,108,116,97,0&gt;&gt;).
&gt; #Fun&lt;erlang.halt.0&gt;
</pre>

Since tryerlang.org doesn't support copy-and-paste from the clipboard, we need to insert the sequence above by hand.

We can bind the binary to a new variable:
<pre>
&gt; B = &lt;&lt;131,113,100,0,6,101,114,108,97,110,103,100,0,4,104,97,108,116,97,0&gt;&gt;.
</pre>

We now need to convert the binary into an Erlang term. Originally, tryerlang.org was allowing <a title="Erlang Safe Binary To Term" href="http://www.erlang.org/doc/man/erlang.html#binary_to_term-2" target="_blank">the binary_to_term function in safe mode</a>. This function has been now completely disabled after this attack. If you want to try what follows you will need to do it in your own Erlang shell.

<pre>
&gt; F = binary_to_term(B, [safe]).
</pre>

Let's now try to launch the fun as:

<pre>
&gt;F().
</pre>

Well, that didn't work as expected. tryerlang.org actually realized that the <code>erlang:halt/0</code> function was going to be called and the sandboxing mechanism managed to block the execution of the command. We need to do something slightly different. For example, we might pass the newly defined fun as an argument (after all, Erlang is a functional language) to a function who would take care of executing it. As an example, we could use the library function <code>lists:map/2</code>. There's only a little tiny problem with that. The <code>list:map/2</code> function, in fact, requires that the fun passed as an argument receives _exactly one argument_. This is not the case of the <code>erlang:halt/0</code> function, which has arity equal to zero. Fortunately <a href="http://www.erlang.org/doc/man/erlang.html#halt-1" target="_blank">an alternative version of <code>erlang:halt/0</code> exists, taking exactly one argument</a>. The external representation for the new function differs from the previous one by only the very last byte. Let's _forget_ the old value of the variable <code>B</code> and let's bind it to the new binary:

<pre>
&gt; f(B).
&gt; B = &lt;&lt;131,113,100,0,6,101,114,108,97,110,103,100,0,4,104,97,108,116,97,1&gt;&gt;.
</pre>

We can now pass the new fun as an argument to the <code>lists:map</code> function:

<pre>
&gt; f(F).
&gt; F = binary_to_term(B, [safe]).
&gt;lists:map(F, [0]).
</pre>

And the node dies. Well, in reality the node is almost immediately brought back by <a title="Erlang Heart" href="http://www.erlang.org/doc/man/heart.html" target="_blank">heart</a> which is listening for heartbeats from the Erlang node itself but, hey, I have to pay a beer to this guy! :)

I wanted to share this experience with all of you. I consider it highly constructive, since it leads to reflect on several aspects of Erlang. Comments and feedback are more than welcome.
