--- 
layout: post
title: "How to manage multiple Erlang installations on the same machine"
date: 2010-11-24 00:00
categories: [erlang, howto, tutorial]
---
Sometimes you need to switch between different versions of the Erlang
runtime system, for example because two of the projects you're
working on require two different Erlang versions. In this post we
will show a way to easily switch between two different versions of the
Erlang runtime system which are installed on the same machine. I've
tested the following approach under Snow Leopard, but the same method should 
be applicable to any UNIX-like system.

When installing
Erlang from source, you can specify a target destination for the
runtime system using the <code>--prefix</code> option for the
<code>configure</code> command:

<pre>
./configure --prefix=YOUR_INSTALLATION_PATH
</pre>

Let's assume that you have installed two different versions of Erlang
in your home directory:

<pre>
$ cd  ~
$ ls
erlang13b04 erlang14a
</pre>

The first thing you need to do is to edit the <code>~/.bashrc</code>
file, by adding the following line to it:

<pre>
PATH=$PATH:$HOME/bin
</pre>

Now create the <code>bin</code> directory under your <code>home</code>:

<pre>
mkdir $HOME/bin
</pre>

Create a new text file and give it the name <code>13</code> (no
extension needed). Fill the file with the following content:

<pre>
#!/bin/bash
env PATH=/User/[USERNAME]/erlang13b04/bin:$PATH &quot;$@&quot;
</pre>

Please adapt the path to the one required by your configuration.

You need to create one script per Erlang installation that you want to
manage. Create a second text file, this time named
<code>14</code>. Fill it with the following content:

<pre>
#!/bin/bash
env PATH=/User/[USERNAME]/erlang14a/bin:$PATH &quot;$@&quot;
</pre>

Again, please adapt the path to the one required by your configuration.

Make the two scripts executable:

<pre>
cd ~/bin
chmod +x 13 14
</pre>

Ensure that the <code>~/.bashrc</code> file is _sourced_ (alternatively, simply open a new shell):

<pre>
source ~/.bashrc
</pre>

That's it. If you want to run a command using R13, just:

<pre>
$ 13 erl
Erlang R13B04 (erts-5.7.5)
Eshell V5.7.5 (abort with ^G)
1&gt;
</pre>

To use version _R14_, instead:

<pre>
$ 14 erl
Erlang R14A (erts-5.8)
Eshell V5.8 (abort with ^G)
1&gt;
</pre>

You can use the script to specify the Erlang version used by a Makefile:

<pre>
$ 13 make
</pre>

Please notice how you can specify the path of a default Erlang installation
in your <code>~/.bashrc</code> file. That will allow you to run a
given Erlang version without explicitly referring it from the command
line.
