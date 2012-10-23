--- 
layout: post
title: "PHP and Emacs. How to Browse Documentation."
date: 2009-12-09 00:00
categories: [browse, doc, documentation, emacs, lisp, mode, php,
php-mode]
---
As an Erlang developer, I spend most of my development time on
Emacs. From time to time I have to hack some PHP code (it's a dirty
job, but someone has to do it), therefore I looked for a way of
browsing the official PHP documentation directly from Emacs.

I couldn't find anything among the existing PHP-modes available that
would allow me to search for a given PHP documentation page from
Emacs and this is why I modified an <a
href="http://forum.trapexit.org/viewtopic.php?p=44248&amp;sid=cfc162ee3e2cbcc16b9af5e20a2bc85a"
target="_blank">existing script</a>, intended to be used with the
Erlang documentation, make it fit the PHP documentation format. The
code is released under GNU GPLv3 license and it's available for
download from my GitHub (TODO) page:

<a href="http://bitbucket.org/roberto.aloi/php-mode/" target="_blank">http://bitbucket.org/roberto.aloi/php-mode/</a>

<a href="http://aloiroberto.files.wordpress.com/2009/12/php2.jpg"><img class="aligncenter size-medium wp-image-193" title="browse-php-doc at work" src="http://aloiroberto.files.wordpress.com/2009/12/php2.jpg?w=300" alt="" width="300" height="181" /></a>

Please note that this tool doesn't prevent you from using any other pre-existing php-mode in conjunction with it.
