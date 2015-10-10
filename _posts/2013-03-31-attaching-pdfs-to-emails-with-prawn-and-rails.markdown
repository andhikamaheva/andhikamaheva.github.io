---
title: Attaching PDFs to emails with Prawn and Rails
author: bcadmin
layout: post
permalink: /work/attaching-pdfs-to-emails-with-prawn-and-rails/
---
Yesterday I released a very simple tool to help copywriters get better briefs. I had a couple of days dev time up my sleeve while other parts of the main <a href="http://csworkflow.com" target="_blank">CS Workflow</a> project are getting worked on.

What I ended up with was a simple signup for copywriters. This generates a token that, when part of a URL, associates the brief with the copywriter. The briefs are a tableless model and are only saved as an attached PDF that is sent to the copywriter. Simple.

I decided to use Prawn over the other options after watching the <a href="http://railscasts.com/episodes/153-pdfs-with-prawn-revised" target="_blank">railscast</a> (requires pro subscription) on the topic. It gave me the most control over the rendered PDF. For this project I used Rail 4.0.0.beta1.

To start I added Prawn to my Gemfile and ran bundle. The latest version was 0.12.0 at writing.

{% highlight ruby %}
gem 'prawn', '~> 0.12.0'
{% endhighlight %}

I found out that through an error message that Rails 4 already has the PDF mimetype registered, so that part of the railscast can be skipped.

I rendered a test PDF in the browser so I could make sure it looked how I wanted before attaching it to an email. Refreshing the browser displayed the changes. To get this working I created a ‘test’ action in my briefs controller and added that as a route.

{% highlight ruby %}
def test
  @brief = Brief.new(test_brief)
  @user = User.find_by_email("ben@csworkflow.com")
  respond_to do |format|
    format.pdf do
      pdf = BriefPdf.new(@brief, @user)
      send_data pdf.render, filename: "brief_#{@brief.name}",
                            type: "application/pdf",
                            disposition: "inline"
    end
  end
end
{% endhighlight %}

Following the same pattern as the railscast, I created a <a href="https://gist.github.com/bchadfield/5274166" target="_blank">BriefsPdf class</a> that inherited from Prawn::Document. This initializes, taking the arguments, which are my objects, then calls methods that render boxes and text. It’s a bit hacked together, but you get the picture. I kept the <a href="http://chadfield.org/assets/brief.pdf" target="_blank">testing output</a>, so that’s what the class renders.

The biggest “gotcha” I came across was with using bounding boxes and text boxes. The cursor, which moves down the page as it renders, behaves differently with those boxes. I ran into trouble with my two bounding boxes, because if the cursor is moved to the bottom of the right box. If the left box is higher I got overlap. With text boxes the cursor doesn’t move down at all. You have to move it manually with move_down. This is fine if you know the height of the box. With user input you don’t have control. That’s why I’m not using text boxes.

The mailer is the simplest part of the whole process.

{% highlight ruby %}
def send_brief(brief, user)
  @brief = brief
  @user = user
  filename = "brief_#{@brief.name.parameterize(sep = '_')}_#{Time.now.strftime('%Y%m%d')}.pdf"
  attachments[filename] = BriefPdf.new(@brief, @user).render
  mail(to: @user.email,
       cc: @brief.email,
       subject: "New brief from #{@brief.name}")
end
{% endhighlight %}

I’m using a dynamic file name for the PDF, so the client and copywriter have a reference. The actual attachment is a single line.

There you have it. I&#8217;ll be using this same technique for creating invoices and subscription agreements.

Here’s the list of resources that guided me:

*   <a href="http://railscasts.com/episodes/153-pdfs-with-prawn-revised" target="_blank">Railscast</a>
*   <a href="http://prawn.majesticseacreature.com/manual.pdf" target="_blank">Prawn documentation</a>
*   <a href="http://guides.rubyonrails.org/action_mailer_basics.html" target="_blank">Action Mailer guide</a>
*   <a href="http://stackoverflow.com/a/14429812" target="_blank">This stackoverflow answer</a>