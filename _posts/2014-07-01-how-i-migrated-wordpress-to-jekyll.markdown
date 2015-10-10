---
title: "How I migrated from Wordpress to Jekyll"
layout: post
description: "How I migrated from Wordpress to Jekyll. A deeper explanation of my tweets as I went through the process."
permalink: /work/how-i-migrated-wordpress-to-jekyll/
---

Last weekend I migrated my personal blog from [Wordpress][1]{:
target="_blank"} to [Jekyll][2]{: target="_blank"}. I tweeted as I went
to keep some sort of record of what I\'d done and the decisions I\'d
made. I also hoped that anyone else wanting to do the same thing would
find it helpful.

It all started because GoDaddy reminded me that my hosting was about to
expire. I\'d been using Jekyll for the CS Workflow site and loved it.

> The hosting on [http://t.co/0WqTirL8Vw][3] is about to expire so today
> I’ll be migrating from wordpress to jekyll and hosting on github
>
> — Ben Chadfield (@benchadfield) [June 28, 2014][4]
{: .twitter-tweet}

That last part about hosting on Github isn\'t true. I hosted it on the
[CS Workflow][5]{: target="_blank"} server.

###  What is Jekyll and why use it?

Jekyll is a static site generator. A static site doesn\'t use any server
side processing. Web browsers can easily handle static HTML, CSS, and
Javascript. You\'ve seen this in action if you have ever double-clicked
a .html file on your desktop and had it opened in your browser.

Jekyll uses a template, processing rules, and content to generate a
static site. Each page of the site has its .html file. The HTML file,
along with the stylesheets, scripts, and images, can be uploaded to any
web server. There are tons of [ways to host static sites][6]{:
target="_blank"} and almost all of them are free.

Wordpress, in comparison, uses PHP and MySQL to generate HTML each time
a Wordpress page is viewed. The template is filled with content from the
database, which is displayed by the browser. This only takes a few
hundredths of a second.

Wordpress makes having a website really easy, especially is you use
[Wordpress.com][7]{: target="_blank"} and don\'t worry about your own
hosting. Almost everything can be managed through the web-based admin
console. You can be completely removed from everything technical, like
HTML markup and installing plugins. Wordpress and platforms like it have
allowed millions of people with no web development skills to have their
own websites. That\'s a great thing!

Why bother with Jekyll then? Jekyll is faster. The site will be faster
to use. Getting a new site setup is faster. Oh, and it supports Markdown
by default. I love faster and I love Markdown, but the main reason I
love Jekyll is that it puts me in total control over my entire site. I
have instant access to style, layout, and content in a single text editor.
I\'m using [Atom][8]{: target="_blank"} for my text editor at the
moment, which I completely recommend.

It\'s totally a preference thing and there is a skills barrier to Jekyll, so it\'s not for
everyone.

###  Exporting from Wordpress

Let\'s get on with it. The migration starts with exporting my content
from Wordpress. I\'d seen in Jekyll\'s documentation that there is
support for migrating. I started there, but the documentation wasn\'t
very thorough and I imagined using their method would waste time.

> Jekyll’s migration docs for wordpress make me think there will be lots
> of messing around with exporting importing [http://t.co/Zc74OpukEI][9]
>
> — Ben Chadfield (@benchadfield) [June 28, 2014][10]
{: .twitter-tweet}

Off to google to find a good guide. I didn\'t want to spend a lot of
time or energy on this migration, so a good tutorial saves both. I
recommend the [how-to guide on girliemac.com][11]{: target="_blank"}.
This is what I followed. I\'ll assume your also using that as a
reference and only chime in if I have something to add.

> This looks like a good how-to guide. I would have forgotten about
> exporting comments. [http://t.co/jIh9JmyHCW][12]
>
> — Ben Chadfield (@benchadfield) [June 28, 2014][13]
{: .twitter-tweet}

One of the first steps was to export comments to Disqus. I didn\'t have
many comments, but I wanted to keep the few I had. I hadn\'t setup
Disqus on a site before. It took than 3 minutes to complete the steps,
going by the twitter timestamps.

Disqus had updated its export/import method and it was even easier that
the way shown in the tutorial. Imports are queued and it took a few
hours before mine were processed.

> Disqus is set up already. So easy. They’ve improved the exporting
> support so there are steps in the how-to I can skip.
>
> — Ben Chadfield (@benchadfield) [June 28, 2014][14]
{: .twitter-tweet}

Jekyll\'s Wordpress exporter accessed the database remotely. The
tutorial uses [wordpress-to-jekyll-exporter][15], a Wordpress plugin.
This plugin isn\'t searchable in the Wordpress plugin directory. I
uploaded the plugin zip file to the plugin folder using FTP. Then I used
the plugin installer in my Wordpress admin console to unzip, install,
and activate the plugin.

> Wordpress to jekyll exporter plugin installed. Export done in one
> click! [https://t.co/NiWVXZIlhX][16]
>
> — Ben Chadfield (@benchadfield) [June 28, 2014][17]
{: .twitter-tweet}

The export was done with one click on the \'Export to Jekyll\' link in
the Wordpress console. This exported my posts and pages to Markdown. It
also added any uploaded media to the export.

My only issue was that it used the .md Markdown extension instead of
.markdown, which I prefer. I used
the view/edit method in Filezilla and did a find and replace in the plugin file to change the .md
to .markdown. I tried to use the plugin editor in the Wordpress console,
but it went crazy when I tried to save the changes.

> The plugin uses .md instead of .markdown which I prefer. I’ve edited
> the plugin and exported again (in one click!)
>
> — Ben Chadfield (@benchadfield) [June 28, 2014][18]
{: .twitter-tweet}

> All exported now to work on the template. I’ll use CS Workflow’s
> preview template builder to get the markup and css.
> [http://t.co/o9tY5rJQCz][19]
>
> — Ben Chadfield (@benchadfield) [June 28, 2014][20]
{: .twitter-tweet}

###  Setting up Jekyll

I didn\'t export my template. I decided to redesign instead. This is
where I wasted the most time. I looked at theme sites for inspiration.

I can\'t remember what I searched for, but I found [Poole][21]{:
target="_blank"}, a Jekyll start kit built by Mark Otto of Bootstrap
fame. Poole already looks pretty good, but has two themes. I used the
[Hyde][22]{: target="_blank"} theme, which I made a few changes to.

* Made the post header an H1. Originally it was an H2 with the site
  title (on the left column) always an H1.
* Changed the blog roll pagination directory from /page2/ to page/2/.
* Removed the pages menu from the left column. I only had the home page,
  so this was unnecessary.
* Removed the special font from the site title in the left and just went
  with the standard PT Sans.
* Added an avatar image for myself.
* Added social icons with links.
* Changed the related posts header from H3 to H4.
* Added a background cover image for the left column. I got the image
  from [this awesome photo resource][23]{: target="_blank"}.
* Increased the font size of the post headers.
* Added a little clock icon next to the post dates.

I think that\'s it. All I needed to do was to copy and paste the export
Markdown files into the `_posts` directory and run `jekyll build`.

> I went with Poole with the Hyde as a Jekyll foundation.
> [http://t.co/LB89E46M0s][24]
>
> — Ben Chadfield (@benchadfield) [June 29, 2014][25]
{: .twitter-tweet}

I needed to host the site myself because there are a few restrictions to
hosting on Github. The main one that stopped me going with that option
is not being able to use plugins. I use two plugins. The first is to
[figure out how old][26]{: target="_blank"} my daughter is. This is
displayed in my bio in the left column. Jekyll uses [Liquid
templates][27]{: target="_blank"}, but doesn\'t come with a timeago
filter as standard. The second plugin is [jekyll-assets][28]{:
target="_blank"}, which compiles the different stylesheets into a
single, minified, gzipped, and cache-busting css file. This makes
loading for the first time even faster.

To start, I created a new Github repository called
[chadfield-blog][29]{: target="_blank"}. This gives me cloud-hosted
source control using git. Github also makes deploying changes really
easy. To get the site on to the server I sshed in and ran `git clone
https://github.com/bchadfield/chadfield-blog.git` from the directory I
wanted to serve the site from. To get any future updates I run `git
pull`.

By default Jekyll generates the site in the `_site` folder. For CS
Workflow I\'d set the build destination to a different directory which
used its own git repository. This time I kept the source and generated
site together.

The trade off of managing a single repository is that I\'m deploying the
source files to the web server and not just the static site. I point the
web server to `/chadfield-blog/_site` instead of `/chadfield-blog` and
have a few extra kilobytes on the server.

All I needed to do was add the site to the Nginx config, restart Nginx,
and point the domain name at the server IP address.
{% highlight nginx %}
server {
 listen 80;
 server_name www.chadfield.org;
 rewrite ^ http://chadfield.org$request_uri? permanent;
}

server {
 listen 80;
 server_name chadfield.org;
 root /home/deployer/chadfield-blog/_site;
 index index.html;
}
{% endhighlight %}

> Finished migrating my Wordpress blog to Jekyll. Here’s the result
> [http://t.co/mh7jjG3fpk][30]
>
> — Ben Chadfield (@benchadfield) [June 29, 2014][31]
{: .twitter-tweet}

###  Publishing workflow

Obviously, the steps to get new content published is different to
Wordpress. I\'ll lay out the steps needs and what I\'ve done to make it
easier.

1.  Write a new post.
2.  Create a new Markdown file in the `_posts` folder.
3.  Add meta-data and content to the Markdown file.
4.  Run `jekyll serve` and test locally that everything is okay.
5.  Commit changes to git using `git add -A`.
6.  Push local git repository to Github using `git push origin master`.
7.  ssh into the server and run `git pull` in the site directory.
8.  Check on my site that the changes are okay.

I automate steps 5, 6, and 7 using a rakefile. I use [CS Workflow][5]{:
target="_blank"} to write, get reviews, and export meta-data to
Markdown.

{% highlight ruby %}
desc "Commit changes to website repo"
task :commit do
	puts "Committing..."
  exec "git add -A && git commit -m 'Site update' && git push origin master"
end

desc "Update code in production"
	task :update do
  puts "Updating production..."
  exec "ssh user@server.com 'cd site-directory && git pull'"
end
{% endhighlight %}


To use that copy into `rakefile.rb` and change the ssh details and site
directory. Then all I need to do is run `rake commit` and `rake update`.

Hopefully you found that helpful. There's plenty of gaps, which is why I've called it
titled it as how I migrated rather than a general how to. Really there's not much to
improve on the how to I referenced. Feel free to ask any questions or offer improvements
I could make.

<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

[1]: http://wordpress.org
[2]: http://jekyllrb.com
[3]: http://t.co/0WqTirL8Vw
[4]: https://twitter.com/benchadfield/statuses/482683466551541760
[5]: http://csworkflow.com
[6]: https://www.google.com.au/search?q=hosting+static+website
[7]: http://wordpress.com
[8]: https://atom.io/
[9]: http://t.co/Zc74OpukEI
[10]: https://twitter.com/benchadfield/statuses/482685148064780288
[11]: http://girliemac.com/blog/2013/12/27/wordpress-to-jekyll/
[12]: http://t.co/jIh9JmyHCW
[13]: https://twitter.com/benchadfield/statuses/482685882965561344
[14]: https://twitter.com/benchadfield/statuses/482686642310746113
[15]: https://github.com/benbalter/wordpress-to-jekyll-exporter
[16]: https://t.co/NiWVXZIlhX
[17]: https://twitter.com/benchadfield/statuses/482687960865714176
[18]: https://twitter.com/benchadfield/statuses/482688323618500608
[19]: http://t.co/o9tY5rJQCz
[20]: https://twitter.com/benchadfield/statuses/482689963738161153
[21]: http://getpoole.com/
[22]: http://hyde.getpoole.com/
[23]: http://nos.twnsnd.co/
[24]: http://t.co/LB89E46M0s
[25]: https://twitter.com/benchadfield/statuses/483111061327863808
[26]: https://github.com/markets/jekyll-timeago
[27]: http://docs.shopify.com/themes/liquid-basics
[28]: https://github.com/ixti/jekyll-assets
[29]: https://github.com/bchadfield/chadfield-blog
[30]: http://t.co/mh7jjG3fpk
[31]: https://twitter.com/benchadfield/statuses/483111432959954944
