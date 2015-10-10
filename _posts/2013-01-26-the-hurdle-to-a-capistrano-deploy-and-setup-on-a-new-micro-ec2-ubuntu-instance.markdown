---
title: The hurdle to a Capistrano deploy and setup on a new micro EC2 Ubuntu instance
author: bcadmin
layout: post
permalink: /work/the-hurdle-to-a-capistrano-deploy-and-setup-on-a-new-micro-ec2-ubuntu-instance/
---
At the end of last year I set myself the challenge of getting <a href="https://github.com/capistrano/capistrano" target="_blank">Capistrano</a> to deploy updates for <a href="https://www.dibbist.com" target="_blank">Dibbist</a>. Two previous attempts had tripped up on the same Rake issues. It was something to do with my server setup and I didn&#8217;t want to start from scratch.

You may have seen <a href="https://twitter.com/OnlineBen/status/275134571937398784" target="_blank">my tweet</a> announcing that I&#8217;d been successful, so you&#8217;ll know I go it working. I did for Dibbist and even more recently repeated the same process for another project I&#8217;m helping out with. This post isn&#8217;t a tutorial on deploying from scratch with Capistrano. I learnt by watching the excellent Railscasts (referenced in my success tweet) about Capistrano. Episode #375 links to the recipes I used. Why no details? These screencasts are part of the paid section of Railscasts and I&#8217;m not going to cut someone&#8217;s lunch, especially Ryan Bates.

This post is about the hurdle I faced twice when following the Railscasts process. Obviously to get a Rails app working you need Ruby installed on the server. The problem I found was that the micro instance took ages to install Ruby. The connection to the server would freeze and Capistrano would just sit there waiting forever for the install to finish. If you looked at the instance activity in the AWS console you&#8217;d see that the CPU had finished with compiling and installing.

The solution is to install Ruby manually at the same time you setup the Deployer user. This will still have the issue with the connection freezing, but once the CPU is finished you&#8217;re done. Just remove the Ruby install from the recipes and run.

The setup I&#8217;m currently using for Dibbist is:

*   EC2 micro instance of Ubuntu 12.04
*   Nginx redirecting all to https
*   Unicorn with 2 workers
*   Postgres