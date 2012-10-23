--- 
layout: post
title: "How to recursively set UNIX permissions for files and directories"
date: 2009-12-04 00:00
categories: [unix, sysadmin, cli, tips and tricks]
---
<a href="http://aloiroberto.files.wordpress.com/2009/12/bsd-linux-devil.jpg"><img class="aligncenter size-medium wp-image-160" title="BSD Devil" src="http://aloiroberto.files.wordpress.com/2009/12/bsd-linux-devil.jpg?w=300" alt="" width="300" height="225" /></a>

Sometimes you need to set specific <a href="http://en.wikipedia.org/wiki/File_system_permissions" target="_blank">UNIX permissions</a> for a whole set of
files and/or directories, in a recursive fashion.

As an example, during the installation process of a Content Management
System such as Joomla or Moodle, you are typically requested to set
permissions of the content of your webroot so that _files_ are readable and writeble only by the
owner and _directories_ are readable, writable and executable only by
the owner. This corresponds to permissions <code>600</code> for
_files_ and <code>700</code> for directories.

This can easily be achieved by entering the webroot (say,
<code>htdocs</code>) and by using the <code>find</code> command:

<pre>
cd htdocs
find . -type f -exec chmod 600 {} +
find . -type d -exec chmod 700 {} +
</pre>

The above commands should be read as follows:

> "Scan everything from the current directory, recursively. For every
  item, if it's a _file_, change its permissions to <code>600</code>;
  if it's a directory, change them to <code>700</code>."

The <code>{} +</code> option executes the specified command to each
item returned by <code>find</code> output. In some sense, it has a
behaviour which is very similar to the one of the <code>xargs</code>
commands. Please refer to the <code>find</code> manual page for more
information.
