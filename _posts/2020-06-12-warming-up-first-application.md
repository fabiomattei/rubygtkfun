---
layout: post
title:  "Warming up: first application"
date:   2020-06-12 23:48:17 +0200
categories: ruby gtk
---

If you installed the gtk3 gem using the command:

{% highlight bash %}
gem install gtk3
{% endhighlight %}

You are ready to create the first GTK3 application.
Type the following commands

{% highlight ruby %}
#!/usr/bin/env ruby

require "gtk3"

app = Gtk::Application.new("org.gtk.example", :flags_none)

app.signal_connect "activate" do |application|
  window = Gtk::ApplicationWindow.new(application)
  window.set_title("My first window")
  window.set_default_size(400, 400)
  window.show_all
end

puts app.run
{% endhighlight %}

If you typed the code correctly and the gtk gem was well installed you should be seeing something like this:

![My first window](/rubygtkfun/images/posts/warming-up.png){:class="aside-image"}
