--- 
layout: post
title: "Emacs Tips and Tricks"
date: 2009-02-19 00:00
categories: [emacs]
---

<h2>Committing files from Emacs</h2>

To commit a single file directly from Emacs, simply follow the steps below:

<ul>
  <li><code>C-x v v</code></li>
  <li>Include a comment</li>
  <li><code>C-c C-c</code></li>
</ul>

<h2>Macros in Emacs</h2>

You can start recording a keyboard macro by typing:

<pre>C-x (</pre>

Do whatever you want and stop recording with:

<pre>C-x )</pre>

Then, you can select a region and type:
<pre>C-x C-k r</pre>

To apply the macro to the selected region.

Emacs Macros are a really powerful tool. Just think if you need to prepend/postpone a string to a group of lines, for example from:

<pre>
First Line
Second Line
Third Line
</pre>

To:

<pre>
<li>First Line</li>
<li>Second Line</li>
<li>Third Line</li>
</pre>

<h2>Words Swapping in Emacs</h2>

Given the following piece of code:

<pre>
foo(First, Second) -&gt;
    ok.
</pre>

Put the cursor on the comma or on the space between <code>First</code>
and <code>Second</code> and press:

<pre>M-t</pre>

You will obtain the following:
<pre>
foo(Second, First) -&gt;
    ok.
</pre>

<h2>Words Swapping in Emacs</h2>

Given the following lines of code:

<pre>
First Line
Second Line
</pre>

Put the cursor at the beginning of the second line and press:
<pre>C-x C-t</pre>

You will get:
<pre>
Second Line
First Line
</pre>

<h2>Running Shell Commands within Emacs</h2>

If you want to run a shell command within Emacs, you can simply type:
<pre>M-!</pre>
If you want to include the output into the current buffer, then:
<pre>C-u M-!</pre>

<h2>Multiple paste</h2>

Sometimes you want to paste some old content from the clipboard, instead of the last copied thing.
In this case, just paste as usual:
<pre>C-y</pre>

Then, browse the clipboard history by typing:
<pre>M-y</pre>

<h2>SVN revert</h2>

If you want to revert your changes to the last revision, just type:
<code>C-x v u</code>

<h2>SVN diff</h2>

If you want to see the differences for a buffer before committing it, just type:
<code>C-x v =</code>

<h2>Numbered lists</h2>

You have a list of items that you would like to convert into a
numbered list. In other words, you want to transform the following text:

<pre>
first
second
third
</pre>

into:

<pre>
1. first
2. second
3. third
</pre>

There are many ways to achieve this, but one is to use <a
href="http://www.gnu.org/software/emacs/manual/html_node/emacs/Keyboard-Macro-Counter.html#Keyboard-Macro-Counter"
target="_blank">the Emacs Keyboard Macro Counter</a>.

Simply follow the steps below:

* Put the cursor one line _above_ your list.
* Start a macro by pressing <code>F3</code>
* Insert the counter value: `C-x C-k C-i`. A <code>0</code> will appear
* Insert a dot and a space: <code>. </code>
* Move the cursor to the next line
* Stop the macro registration by pressing <code>F4</code>
* Select the itmes that you want to convert into a numbered list
* Press: <code>M-x apply-macro-to-region-lines</code>
* You can delete the <code>0</code> you added on the top and enjoy :)
