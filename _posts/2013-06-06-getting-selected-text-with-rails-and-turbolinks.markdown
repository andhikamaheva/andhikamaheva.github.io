---
title: Getting selected text with Rails and Turbolinks
author: bcadmin
layout: post
permalink: /work/getting-selected-text-with-rails-and-turbolinks/
---
I have to start by confessing that I don&#8217;t know what it is about Turbolinks that caused the issue I was having. I&#8217;m only edu-guessing that Turbolinks is the cause.

So&#8230;I needed to know the text that the user had selected with their cursor. This would be used to create context for the comment they wanted to make on the text. I started by using <a href="http://stackoverflow.com/questions/5379120/get-the-highlighted-selected-text" target="_blank">a popular method I found on Stack Overflow</a>.

{% highlight javascript %}
function getSelectionText() {
  if (window.getSelection) {
    return window.getSelection().toString();
  } else if (document.selection && document.selection.type != "Control") {
    return document.selection.createRange().text;
  }
}
{% endhighlight %}

This worked fine in a static proof of concept. It also initially worked in my Rails project. By initially I mean after a browser refresh. As soon as I navigated to other pages and retested the function fell through and returned nothing. The rest of my javascript is fine. I am displaying a positioned button after text is selected and once clicked, the button performs an action with the selected text. This all works as expected.

I don&#8217;t know enough about the DOM or getSelection method to figure it out on my own. I set Google on it, which turned up a <a href="http://www.codeproject.com/Articles/292159/Javascript-code-to-get-selected-text" target="_blank">different function from the rest</a>.

{% highlight javascript %}
function GetSelectedText() {
  var selectedText = (
    window.getSelection
    ?
      window.getSelection()
    :
      document.getSelection
      ?
        document.getSelection()
      :
        document.selection.createRange().text
  );
  if (!selectedText || selectedText=="") {
    if(document.activeElement.selectionStart) {
      selectedText = document.activeElement.value.substring(
        document.activeElement.selectionStart
        . document.activeElement.selectionEnd);
    }
  }
  return selectedText;
}
{% endhighlight %}

That is now working. Or at least it fixes my previous bug. It&#8217;s the nested if where selectedText is blank that solves it. I don&#8217;t like the if else in the selectedText initiation so I&#8217;m using the original function is start with.