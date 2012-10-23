--- 
layout: post
title: "Mercurial - Verbose Pull"
date: 2009-09-16
categories: [mercurial, tips and tricks, productivity]
---
Are you pulling from a Mercurial repository and it's taking too long?
Do you want to know which files are being pulled into your local
machine while you wait for the pulling process to complete? Did you
try <code>hg --verbose pull</code> and it didn't work as expected?

Then try the following:

<pre>
hg --debug -v pull
</pre>
