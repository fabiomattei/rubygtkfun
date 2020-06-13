---
layout: post
title:  "Labels and output"
date:   2020-06-14 12:00:00 +0200
categories: basics
tags: output label
---

![My first window](/rubygtkfun/images/posts/label.png){:class="aside-image"}

Sometimes we need to give some information to a user, we need to send some output or we need just to write some text in order to help him using the interface.

This is when the label widget becomes handy.

{% highlight ruby %}
#!/usr/bin/env ruby

require 'gtk3'

app = Gtk::Application.new("org.rubygtkfun.label", :flags_none)

app.signal_connect "activate" do |application|
  window = Gtk::ApplicationWindow.new application
  window.set_title "My first window with a label"
  window.set_default_size 400, 400

  label = Gtk::Label.new 'My brand new label'
  window.add label

  window.show_all
end

puts app.run

{% endhighlight %}


The code you see here is so similar to the code you have seen in the [previous article](www.example.com), I added just two more lines.


### Adding a label

{% highlight ruby %}
label = Gtk::Label.new 'My brand new label'
window.add label
{% endhighlight %}


