---
layout: post
title: "How to Checkout GitHub Pull Requests Locally"
date: 2012-11-12 10:36
comments: true
categories: [git, github, productivity]
---

I've recently bumped into the following useful <a href="https://gist.github.com/3342247" target="_blank">gist</a>, which I decided to share with all of you.

It's possible to instruct git to fetch pull requests together with the other project branches. Simply open the `.git/config` file for your project and add the following line under the `[remote "origin"]` section:

    fetch = +refs/pull/*/head:refs/remotes/origin/pr/*

To enable this behaviour for all of your git projects, simply run:

    git config --global --add remote.origin.fetch "+refs/pull/*/head:refs/remotes/origin/pr/*"

To fetch all the pull requests for a project:

    git fetch origin

To checkout a specific pull request (say, #53):

    git checkout pr/53

Enjoy!
