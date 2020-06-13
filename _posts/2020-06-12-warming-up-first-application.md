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
Create a new file named **warming-up.rb** and type the following commands

{% highlight ruby linenos %}
#!/usr/bin/env ruby

require "gtk3"

app = Gtk::Application.new("org.rubygtkfun.warmingup", :flags_none)

app.signal_connect "activate" do |application|
  window = Gtk::ApplicationWindow.new(application)
  window.set_title("My first window")
  window.set_default_size(400, 400)
  window.show_all
end

puts app.run
{% endhighlight %}

Now we can give to the file we just created execution privileges:
{% highlight bash %}
chmod +x warming-up.rb
{% endhighlight %}

Now we can run it:
{% highlight bash %}
./warming-up.rb
{% endhighlight %}

If you typed the code correctly and the gtk gem was well installed you should be seeing something like this:

![My first window](/rubygtkfun/images/posts/warming-up.png){:class="aside-image"}

It means you did well, the application is running and you build your first ruby gtk application.
Congratulations!!

Let's see what have we type line by line.

The shebang in the first line helps us to define which interpreter must be used to execute the script under UNIX/Linux operating systems.

### First code block
We import the gtk3 library.

### Second code block
We initialize a new application writing: 
app = Gtk::Application.new("org.rubygtkfun.warmingup", :flags_none)

The initializer takes two parameters:

* org.rubygtkfun.warmingup: this is our application’s id and in general it should be a reverse DNS style identifier. For more information about its usage check out [the gnome documentation about the](https://wiki.gnome.org/HowDoI/ChooseApplicationID)

* :flags_none: this is a flag defining the behavior of the application. In our case, we used the default behavior. [There are many types of application you can define](https://lazka.github.io/pgi-docs/GObject-2.0/flags.html#GObject.GFlags). 

### Third code block
The following block of code connect the application [signal](http://ruby-gnome.sourceforge.net/programming/signal.html) named **activate** to the following commands. Gtk library is driven by signals. Gtk programming consists, in large part, in setting signals handlers. When the **activate** signal is received the following lines of code create a new window, give to this window a title and a size and show the window.

