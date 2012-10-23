--- 
layout: post
title: "Mercurial - Gnome Keyring Integration"
categories: [mercurial, hg, gnome, productivity]
---
Don't know about you, but I find really boring having to insert my
password over and over again when pulling hg-based projects.

If you are using Gnome, you can integrate Mercurial with the Gnome Keyring.

Simply <a
href="http://bitbucket.org/ebo/hggnome-keyring/changeset/4f8cbce98fe6/"
target="_blank">download this Mercurial extension</a> and install it,
by adding the following line to the <code>[extensions]</code> block of
your <code>.hgrc</code> file:

<pre>
hggnome-keyring = [PATH_TO_EXTENSION]/hggnome-keyring.py
</pre>

Remember to adjust the `PATH_TO_EXTENSION` to the path where you
installed the extension.

From now on, whenever pulling from a hg repo, the system will prompt
you for the password just on the first time.

