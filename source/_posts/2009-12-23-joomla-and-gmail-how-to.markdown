--- 
layout: post
title: "Joomla and Gmail How To"
date: 2009-12-23 00:00
categories: [joomla, gmail, php]
---
A couple of weeks ago, I decided to use Gmail as SMTP server to send
emails from my Joomla website. Here is explained what I did to make
everything working.

First of all, I edited my <code>configuration.php</code> file to
contain the following settings:

<pre>
var $mailer = 'SMTP Server';
var $mailfrom = 'MY_GMAIL_ADDRESS';
var $smtpauth = '1';
var $smtpuser = 'MY_GMAIL_ADDRESS';
var $smtppass = 'MY_GMAIL_PASSWORD';
var $smtphost = 'ssl://smtp.gmail.com:465';
</pre>

Then, I patched the <code>libraries/phpmailer/phpmailer.php</code>
file by editing the <code>SmtpConnect</code> function. In the specific
I changed the lines:

<pre>
if(strstr($hosts[$index], ":"))
  list($host, $port) = explode(":", $hosts[$index]);
</pre>

into:

<pre>
if (preg_match('#(([a-z]+://)?[^:]+):(\d+)#i', $hosts[$index],
$match)) {
  $host = $match[1];
  $port = $match[3];
}
</pre>

Please note that I'm using Joomla version 1.5.6. The solution is based
on <a href="http://byet.net/showthread.php?t=7142"
target="_blank">this discussion thread</a>.
