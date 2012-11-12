---
layout: post
title: "Emacs Tips and Tricks"
date: 2009-02-19 00:00
categories: [emacs]
comments: true
---

In this blog post I collect some miscellaneous Emacs tips and tricks.

<h2>Playing with Macros</h2>

In Emacs, you can _record_ a set of actions that you can then apply to a selected region. As an example, let's transform the following three lines:

<pre>
First Line
Second Line
Third Line
</pre>

into a list of items, using a macro:

<pre>
- First Line
- Second Line
- Third Line
</pre>

Put your cursor on the <code>First line</code>, then start recording a new keyboard macro by typing:

<pre>C-x (</pre>

Jump to the beginning of the line (<code>C-a</code>), insert a dash followed by a space (<code>- </code>) and then move your cursor down one line, so it resides on the <code>Second Line</code>.

Stop recording the macro:

<pre>C-x )</pre>

Now select the lines <code>Second Line</code> and <code>Third Line</code> and apply the newly recorded macro to the selected region by pressing:

<pre>C-x C-k r</pre>

You should now see the desired output.

<h2>Swapping Words</h2>

Say that you want to reverse the order of the parameter for the following function:

<pre>
foo(Second, First) -&gt;
    ok.
</pre>

Position the cursor between the words <code>Second</code> and <code>First</code>. Then, press:

<pre>M-t</pre>

You should obtain the following:

<pre>
foo(First, Second) -&gt;
    ok.
</pre>

<h2>Swapping Lines</h2>

Given the following two lines:

<pre>
Second Line
First Line
</pre>

Put the cursor at the beginning of <code>First Line</code> and press:

<pre>C-x C-t</pre>

You should get:

<pre>
First Line
Second Line
</pre>

<h2>Version Control</h2>

Emacs has support for the most common Version Control systems (e.g. _SVN_).

To check-in a single file directly from Emacs, simply follow the steps below:

* Press <code>C-x v v</code>
* Write a meaningful _change comment_
* Press <code>C-c C-c</code>

To revert changes for the current buffer:

<code>C-x v u</code>

To see the differences for a buffer before committing it:

<code>C-x v =</code>

<h2>Executing a Shell Command</h2>

If you want to execute a shell command within Emacs, you can simply type:

<pre>M-!</pre>

If you want to include the output into the current buffer, then:

<pre>C-u M-!</pre>

<h2>Clipboard History</h2>

Emacs keeps a clipboard history, allowing you to paste old clipboard entries. To utilize this function:

Press the following to paste:

<pre>C-y</pre>

And then browse the clipboard history by repeatedly typing:

<pre>M-y</pre>

<h2>Create a Numbered List</h2>

Say that you have a list of items that you want to convert into a numbered list:

<pre>
first
second
third
</pre>

<pre>
1. first
2. second
3. third
</pre>

There are many ways to achieve this. One is to use <a
href="http://www.gnu.org/software/emacs/manual/html_node/emacs/Keyboard-Macro-Counter.html#Keyboard-Macro-Counter"
target="_blank">the Emacs Keyboard Macro Counter</a>.

Position the cursor one line _above_ your list and start registering a new macro:

<pre>C-x (</pre>

Insert a new counter value:

<pre>C-x C-k C-i.</pre>

A <code>0</code> will appear. Append a dot and a space:

<pre>. </pre>

Move the cursor to the next line and stop registering the macro:

<pre>C-x )</pre>

Select the list of items and apply the macro to the selected region:

<pre>C-x C-k r</pre>

Delete the <code>0</code> that you added at the beginning of the list and enjoy your brand new numbered list.
