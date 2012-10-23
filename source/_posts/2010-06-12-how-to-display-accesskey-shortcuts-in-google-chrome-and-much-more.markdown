--- 
layout: post
title: "How to Display accesskey shortcuts in Google Chrome (and much
more)"
date: 2010-06-12 00:00
categories: [access key, accesskey, chrome, chromium, extension, google,
guide, howto, shortcut, shortcuts, tutorial, accessibility]
---

Have you ever heard about <a
href="http://en.wikipedia.org/wiki/Access_key" target="_blank">access
keys</a>? Well, I did. And I loved them. Your productivity gets such a
boost when using shourtcuts rather than the mouse when browsing the web.

The bad thing about access keys is that they're often hidden, by
default, in the web pages. This doesn't make sense to me.

Take the Twitter home page as an example. How many of you knew that, during a search, you could press <code>CTRL+ALT+n</code> to display the <code>"N new tweets since you started searching"</code> or that you could press <code>CTRL+ALT+s</code> to visit your "settings" page? As a different example, let's consider Wikipedia. Did you know that <code>CTRL+ALT+e</code> lead you to the "edit" mode? Probably not.

Resuming, "accesskey" shortcuts can be very useful. So why they are not displayed by default on the web pages? How should we know about them? And how could we ever remember all of them?

Long time ago, I found <a href="http://blog.andrewbeacock.com/2007/06/firefox-hack-to-display-accesskey.html" target="_blank">this post </a>on how to display the "accesskey" keyboard shortcuts in Firefox and I used it for a while. But I've recently fallen in love with Google Chrome and I was wondering if the same feature was already available.

At first, I googled for a quick solution and I couldn't find anything really useful. Then, <a href="http://superuser.com/questions/141142/displaying-the-accesskey-keyboard-shortcuts-in-chrome-mac" target="_blank">I asked on Superuser if what I wanted was somehow possible</a>. After a couple of hours, someone answered my question, claiming he created a new Chrome extension just for that. I must admit I was more impressed by the rapidity of the answer than by the answer itself. If this guy could read my specification and implement a solution in such a short time, there was only one possible consequence: <strong>"Creating extension for Google Chrome is easy"</strong>.

So, I tried by myself.

First of all, I had a look <a href="http://code.google.com/chrome/extensions/getstarted.html" target="_blank">to the "Getting Started" section of the Chrome extensions documentation</a>. As expected, everything was extremely simple. To implement the "accesskey" shortcuts, it took me no more than five minutes. Literally. And now my Twitter page looks like:
<p style="text-align:center;"><a href="http://aloiroberto.files.wordpress.com/2010/06/screen-shot-2010-06-11-at-11-59-19-pm.png"><img class="aligncenter size-medium wp-image-339" title="My new Twitter Home Page" src="http://aloiroberto.files.wordpress.com/2010/06/screen-shot-2010-06-11-at-11-59-19-pm.png?w=300" alt="" width="300" height="173" /></a></p>
Can you see the pink characters close to the links? They are all available "accesskey" shortcuts, a piece of information that was already embedded in the web page but that has just been hidden. Let's see how can we make it visible again via a brand new Google Chrome Extension.

First of all, <strong>create a new folder</strong> somewhere in your hard drive and call it "shortcuts".

Every Chrome extension is characterized by a "manifest" file, written in json, reporting the "properties" of the extension itself. Inside the "shortcuts" folder, <strong>create a new file, named "manifest.json"</strong>:

<pre>
{
  "name": "Shortcuts",
  "version": "1.0",
  "description": "Display the accesskey shortcuts.",
  "content_scripts": [{
    "matches": ["http://*/*", "https://*/*"],
    "css": ["style.css"]
  }]
}
</pre>

Apart from the name, the version number and the description of the extension, you can notice a "content_scripts" property. This is used to "inject" some code automatically every time a web page is displayed. In our case, we simply want to apply some specific CSS properties to the pages. The "matches" section tells Chrome to apply the transformation to every page using the http or the https protocol.

Now, we just need to <strong>create a style.css file</strong> (inside
the same "shortcuts" folder) containing the needed stylistic
information:

<pre>
a[accesskey]:after,
button[accesskey]:after,
input[accesskey]:after,
label[accesskey]:after,
legend[accesskey]:after,
textarea[accesskey]:after {
  margin-left: 0.3em;
  color: Plum;
  content: "[" attr(accesskey) "]";
}
</pre>

That's all folks. We're done. We can just install our brand new Google Chrome Extensions by visiting the URL:

<address>chrome://extension</address>and clicking on the "Load Unpacked Extension" button.

Using the same strategy, it is obviously possible to apply different
CSS transformations. Imagine for a second that you would like to hide
all the images from a web page. A CSS like the following would do the
job:

<pre>
img {
  display: none;
}
</pre>

Hope this help.
