--- 
layout: post
title: "The growth of Erlang: The Stack Overflow Case Study"
date: 2010-12-11 00:00
categories: [erlang]
---

#  image_url: #http://aloiroberto.files.wordpress.com/2010/12/screen-shot-2010-12-11-at-2-40-55-pm1.png

One of the most popular technical _Questions and Answers_ websites is nowadays represented by <a href="http://www.stackoverflow.com">Stack Overflow</a>. Compared to a more traditional mailing list, it provides different advantages:

<ul>
	<li>More structured information</li>
	<li>Focus on the problem/issue</li>
	<li>Information easier to find</li>
	<li>Threads easier to follow</li>
	<li>Concept of reputation (most active users "rewarded")</li>
	<li>Etc.</li>
</ul>

Please note that I'm not suggesting Stack Overflow as a mere _replacement_ for every existing mailing list. I rather feel that the two tools may coexist. In fact, they have two completely  different targets.

<ul>
	<li>Technical problem/issue -&gt; Stack Overflow</li>
	<li>Open discussion -&gt; Mailing list</li>
</ul>

Recently, I've noticed an increased number of posts tagged _Erlang_ on Stack Overflow. I then asked myself:

<ol>
	<li>How is Erlang growing on Stack Overflow?</li>
	<li>How the Stack Overflow growth is affecting the Erlang mailing list?</li>
	<li>How is Erlang growing on Stack Overflow in relation to mainstream languages, such as C++, Java or PHP?</li>
	<li>How is Erlang growing on Stack Overflow in relation to non-mainstream languages, such as Scala, Haskell or Go?</li>
</ol>

Then, I've tried to give an answer to all of these questions.

<h2>How is Erlang growing on Stack Overflow?</h2>

You might not be aware of this, but <a target="_blank" href="http://odata.stackexchange.com">odata.stackexchange.com</a> allows you to run arbitrary SQL queries on the Stack Exchange family of sites, of which Stack Overflow is part. Therefore, I decided to write my first query, asking Stack Overflow about the trend of posts tagged _Erlang_ over time. The query is parametrical, so you can use it to verify the trend of _any_ tag on Stack Overflow. Also, since I'm new to my SQL Server, you are very welcome to edit and to make more efficient <a target="_blank"  href="http://data.stackexchange.com/stackoverflow/s/708/how-many-posts-per-month-for-a-tag">my query</a>.

Plotting the query results into a graph result in the following:

<a href="http://aloiroberto.files.wordpress.com/2010/12/screen-shot-2010-12-11-at-2-40-55-pm1.png"><img class="aligncenter size-full wp-image-459" title="Erlang Posts on Stack Overfow" src="http://aloiroberto.files.wordpress.com/2010/12/screen-shot-2010-12-11-at-2-40-55-pm1.png" alt="Erlang Posts on Stack Overfow" width="540" height="320" /></a>

Where the x-axis ranges from August 2008 to October 2010.

<h2>How is the Stack Overflow growth affecting the Erlang mailing list?</h2>

<a title="Gmane" href="www.gmane.org" target="_blank">Gmane</a> offers a whole set services related to mailing lists. Among these, it provides some really interesting statistics on the mailing list usage. The following graphs show the number of messages and the participants per day for the _Erlang General_ mailing list for the past few years. You can find more details about the mailing list <a href="http://gmane.org/details.php?group=gmane.comp.lang.erlang.general">here</a>.

<a href="http://aloiroberto.files.wordpress.com/2010/12/screen-shot-2010-12-11-at-2-50-46-pm.png"><img class="aligncenter size-full wp-image-460" title="Activity on the Erlang General Mailing List" src="http://aloiroberto.files.wordpress.com/2010/12/screen-shot-2010-12-11-at-2-50-46-pm.png" alt="" width="507" height="326" /></a>

From the graph, it looks like the recent growth of Stack Overflow didn't affect significantly the usage Erlang mailing list, even if you can notice a tiny decrease in the mailing list usage in the final section of the graph (years 2008/2009). Of course other factors might play an important role affecting the graph.

<h2>How is Erlang growing on Stack Overflow in relation to mainstream languages, such as C++, Java or PHP?</h2>

A graph is worth a billion words.

<a href="http://aloiroberto.files.wordpress.com/2010/12/screen-shot-2010-12-11-at-3-11-55-pm.png"><img class="aligncenter size-full wp-image-464" title="Erlang VS C++, Java and PHP" src="http://aloiroberto.files.wordpress.com/2010/12/screen-shot-2010-12-11-at-3-11-55-pm.png" alt="Erlang VS C++, Java and PHP" width="540" height="320" /></a>

<h2>How is Erlang growing on Stack Overflow in relation to non-mainstream languages, such as Scala, Haskell or Go?</h2>

<a href="http://aloiroberto.files.wordpress.com/2010/12/screen-shot-2010-12-11-at-3-11-18-pm.png"><img class="aligncenter size-full wp-image-465" title="Erlang VS Scala, Haskell and Go" src="http://aloiroberto.files.wordpress.com/2010/12/screen-shot-2010-12-11-at-3-11-18-pm.png" alt="Erlang VS Scala, Haskell and Go" width="540" height="319" /></a>

<h2>Conclusions</h2>

Comparing Erlang with mainstream languages, such as PHP, C++ or Java is probably a bit _unfair_. Compared with other languages belonging to the same family, it shows an exponential growth which is conforting. I just hope you enjoyed reading this simple case study as much as I enjoyed writing it. Feel free to play with my query. Comments and opinions are always welcome.
