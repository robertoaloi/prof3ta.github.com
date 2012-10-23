--- 
layout: post
title: "How to integrate Firefox and Emacs"
date: 2010-01-23 00:00
categories: [emacs, firefox, edit, howto, textarea, textbox, productivity]
---
<p style="text-align:center;"><a href="http://www.gnu.org/software/emacs/"><img class="aligncenter size-medium wp-image-250" title="Emacs Logo" src="http://aloiroberto.files.wordpress.com/2010/01/emacs.png?w=300" alt="Emacs Logo" width="240" height="196" /></a></p>
Sometimes, when you edit a <strong>textarea</strong> on a web page (for example, to write a new post on your blog), you would really like to use an external text editor for that.

I personally love <strong>Emacs</strong>, I'm addicted to its shortcuts and key bindings and I would love to use it, for example, for searching and replacing or for applying macros on the text of a textarea.

Well, it seems someone already thought about this. A <strong>Firefox plugin</strong> to bind an external editor to your browser is available <a href="https://addons.mozilla.org/en-US/firefox/addon/4125" target="_blank"><strong>here</strong></a>. In the following lines, I'll refer to a <strong>Linux</strong> environment, but the same procedure, by applying some variants, is possible on <strong>Mac</strong>, too.

Once installed the plugin and restarted Firefox, you might want to edit some <strong>preferences</strong>.

First of all, specify the following <strong>command</strong> to be executed:
<pre>/usr/bin/emacsclient</pre>
The reason we don't simply trigger the <em>emacs</em> command, but we use <em>emacsclient</em> instead is that, if we have an Emacs session open, we would like to attach to that one, so we could easily move between Emacs buffers (thanks to Magnus for this suggestion).

Before this can actually work, though, we need to start a daemon on Emacs. To do so, just open Emacs and do the following:
<ul>
	<li>M-x customize-option</li>
	<li>Variable name: server-mode</li>
	<li>Click on toggle</li>
	<li>Save for future sessions</li>
	<li>Finish</li>
</ul>
Optionally (and I would strongly advise you to do so), you can bind the trigger of the external editor to a <strong>shortcut</strong>. I personally use the following:
<pre>Alt + E</pre>
But this is obviously up to you.

That's it. You can enjoy editing your text areas in Emacs and make your productivity fly high.
