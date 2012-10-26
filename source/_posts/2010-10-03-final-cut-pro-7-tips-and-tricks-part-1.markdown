---
layout: post
title: "Final Cut Pro 7 - Tips and Tricks"
date: 2010-10-03 00:00
categories: [apple, mac, osx, final cut, final cut 7 pro, tips, tricks, video editing]
published: false
---
TODO
<a href="http://aloiroberto.files.wordpress.com/2010/10/finalcut.jpg"><img class="aligncenter size-full wp-image-370" title="Final Cut Pro 7" src="http://aloiroberto.files.wordpress.com/2010/10/finalcut.jpg" alt="Final Cut Pro 7 Logo" width="180" height="189" /></a></p>

<h2>1. Personal Settings and Preferences</h2>

As soon as you start working with Final Cut Pro, you realize how
useful it is to customize toolbars, layouts and preferences.
All of these customizations are stored in:

<pre>
~/Library/Preferences/Final Cut Pro User Data/
</pre>

To restore Final Cut's original settings just delete all the files
contained in the above directory, exception made for
the <code>plugin/</code> directory, which contains all the installed
Final Cut plugins. To re-use your favourite Final Cut Pro settings on a
different machine, spend a couple of minutes by copying the setting files
onto the new machine. That will boost your productivity tremendously.

<h2>2. Focus on the Right Panel</h2>

To switch between the _Viewer_, the _Canvas_, the _Timeline_ and the _Browser_, use the _show/hide_ keyboard shortcuts and save yourself plenty of time:

<pre>
Cmd-1 -&gt; Focus on the Viewer
Cmd-2 -&gt; Focus on the Canvas
Cmd-3 -&gt; Focus on the Timeline
Cmd-4 -&gt; Focus on the Browser
</pre>

<h2>3. The three most common windows layouts</h2>

Sometimes you mainly work on the _Viewer_. Some other times most of your work
is performed on the _Canvas_. Sometimes you want to see all panels simultaneously. Take five minutes of your time to set the three most common windows layouts as your custom layouts and use shortcuts to switch among them.

<ol>
  <li>Enlarge the viewer and save the window layout as your custom layout 1 (from the _window_ menu). You can recall this layout at any time with: <code>Shift-U</code></li>
  <li>Now enlarge the canvas and save the new window layout as your custom layout 2. You can recall it by hitting:<code>Option-U</code></li>
  <li>Go back to the default view via:<code>Ctrl-U</code></li>
</ol>

<h2>4. Scrubber quickly, easily!</h2>

You can use the <code>J-K-L</code> keys to play a clip or a sequence
backward of forward:

<pre>
J -&gt; Play backward
K -&gt; Stop playing
L -&gt; Play forward
J-K -&gt; Play backward in slow motion
K-L -&gt; Play forward in slow motion
K-tap J -&gt; Play backward one frame at the time
K-tap L -&gt; Play forward one frame at the time
</pre>

Also, press the <code>SHIFT</code> key to use seconds instead of frames as basic measurement unit for movements.

<h2>5. Don't scrubber audio, if you don't need it</h2>

Use <code>Shift-s</code> to enable or disable audio-scrubbing.

<h2>6. Synchronize video tracks based on the audio</h2>

Save yourself hours in postproduction by installing the <a title="Final Cut Plural Eyes Plugin" href="http://www.singularsoftware.com/pluraleyes.html" target="_blank">pluraleyes plugin</a> (149$) to do this.

<h2>7. Avoid rendering during preview</h2>

Bored about the red bars on the top of the timeline which inform you
that the video can't be played without rendering? You're probably
working in Safe RT mode. On the top-left corner of the timeline, hit
the RT button and select RT Unlimited. Also, adjust the remaining
values to "Dynamic". This will tell Final Cut to preview as many
effects in the sequence as it can.

<h2>8. Moving in the timeline</h2>

Did you know that, when you are in the timeline, you can just start
typing a number to move the playhead at that exact position? The
number represents the number of frames you want to move by. If you
want to use seconds, instead, just append a DOT at the end of the
number.

<pre>
5 -&gt; 5 frames
5. -&gt; 5 seconds
</pre>

<h2>9. Delete clips without leaving a gap</h2>

This operation is known as "ripple delete". Use the forward delete
button (or FN + Delete if you're on a laptop) to delete a clip and
ripple the rest of the sequence. Toggle the ripple markers button (on
the top-right corner of the timeline) according to the desired
behaviour.


<h2>10. Preview in Full Screen</h2>

In the Final Cut Pro Menu, set the following:

<pre>
View -&gt; Video Playback - &gt;Digital
View -&gt; External Video -&gt; All frames
</pre>

Now you can preview your piece of artwork in full screen by hitting <code>Cmd-F12</code>.

<strong>Stay tuned for more Final Cut tips and tricks!</strong>
