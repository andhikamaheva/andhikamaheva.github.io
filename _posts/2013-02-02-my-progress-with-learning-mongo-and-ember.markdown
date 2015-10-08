---
title: My progress with learning Mongo and Ember
author: bcadmin
layout: post
permalink: /work/my-progress-with-learning-mongo-and-ember/
---
I&#8217;ve spent about 16 hours running through tutorials, reading and rebuilding <a href="http://www.poopee.com.au" target="_blank">Poopee</a>. This post will cover what I&#8217;ve learnt so far and how.

Poopee currently uses a MySQL database fronted by PHP that returns XML. The front-end is JQuery. My aim is to rebuild it with Mongo and Ember.

### <a href="http://www.mongodb.org/" target="_blank">MongoDB</a>

I&#8217;m comfortable with Mongo. I run through a basic <a href="http://tutorial.mongly.com/tutorial/index" target="_blank">interactive tutorial</a> at <a href="http://mongly.com" target="_blank">Mongly</a>. The main reason I wanted to use Mongo was that it had a simple way to handle <a href="http://docs.mongodb.org/manual/core/geospatial-indexes/" target="_blank">geospatial queries</a>. This was covered by Mongly with a <a href="http://tutorial.mongly.com/geo/index" target="_blank">geospatial tutorial</a>.

The next step was to learn how to use Mongo as part of an API. <a href="http://coenraets.org/blog/" target="_blank">Christophe Coenraets</a> has a good two-part tutorial on how to build a simple site with <a href="http://nodejs.org/" target="_blank">Node.js</a>, <a href="http://expressjs.com/" target="_blank">Express</a>, Mongo and <a href="http://backbonejs.org/" target="_blank">Backbone</a>. The first part is a good guide on <a href="http://coenraets.org/blog/2012/10/creating-a-rest-api-using-node-js-express-and-mongodb/" target="_blank">building the API</a>, which I followed. The second is really a link to a github repository for the finished product. I used the first post to build the API for Poopee. That included importing the lastest batch of Australian Toilet data. Importing the XML data was the single task that I spent the most time on.

### <a href="http://emberjs.com/" target="_blank">Ember</a>

Outside the day and a half I spent on the API, I read about the good, bad and the ugly of pretty much every javascript framework I could find. I settled on Ember as the framework that I&#8217;d tackle. Ember is popular enough to have documentation and good tutorials. The decision was a toss-up between <a href="http://angularjs.org/" target="_blank">Angular</a> and Ember. I rejected Angular because I didn&#8217;t like the way it extended HTML. I prefer to keep my HTML clean. Obviously, I can change my mind later, once I delve deeper into Ember. It&#8217;s highly likely I&#8217;ll end up using Backbone for Poopee, because it&#8217;s such a straight forward web app.

So far, I&#8217;ve spent my time coming to grips with the new (to me) concepts in Ember. After reading the <a href="http://emberjs.com/guides/" target="_blank">Ember guides</a>, the article/tutorial that I saw recommended was <a href="http://trek.github.com/" target="_blank">Advice on &#038; Instruction in the Use Of Ember.js</a>.

The next step is to run the <a href="http://reefpoints.dockyard.com/ember/2013/01/07/building-an-ember-app-with-rails-api-part-1.html" target="_blank">Ember and Rails tutorials</a>. The concept that I struggled with was how the API connection worked with the routing. I&#8217;m expecting this tutorial to help me understand that.