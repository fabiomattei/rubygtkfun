---
layout: post
title:  "Box container"
date:   2020-06-20 12:00:00 +0200
categories: basics
tags: box container
---

![Entry widget](/rubygtkfun/images/posts/box.png){:class="aside-image"}

Up to now we learned how to use some basic widget, we learned how to initialize an Entry, a Label 
and a Button. It is time for us to learn how to position **widgets** in a window.

We need to learn to use **containers**.

As you can see in this [Gnome documentation containers list page](https://developer.gnome.org/gtk3/stable/LayoutContainers.html) 
there are many containers we can use in order to position our [widgets](https://developer.gnome.org/gtk3/stable/ch03.html) 
in a window.

Today we are going to introduce the **Box**.

The Box container allow me to position a set of widgets in a row. The row can be vertical or horizontal.

{% highlight ruby %}
#!/usr/bin/ruby

'''
This example demonstrates the Gtk::Box container.

Author: Fabio Mattei
Website: https://fabiomattei.github.io/rubygtkfun
Last modified: June 2020
'''

require 'gtk3'

class Application < Gtk::Application

  def initialize
    super 'org.rubygtkfun.box', Gio::ApplicationFlags::FLAGS_NONE

    signal_connect :activate do |application|
      window = Gtk::ApplicationWindow.new application
      window.set_default_size 300, 100
      window.set_title 'Example of a box container'

      box = Gtk::Box.new :horizontal # it could be :vertical too
      window.add box

      @hello_button = Gtk::Button.new :label => "Hello"
      box.add @hello_button

      @world_button = Gtk::Button.new :label => "World"
      box.add @world_button

      @label = Gtk::Label.new 'Still empty!'
      box.add @label

      @hello_button.signal_connect "clicked" do |sender, event| 
        on_btn_clicked sender, event
      end

      @world_button.signal_connect "clicked" do |sender, event| 
        on_btn_clicked sender, event
      end

      window.show_all
    end

  end

  def on_btn_clicked sender, event
    @label.text= sender.label
    puts "clicking: " + sender.label
  end

end


app = Application.new

puts app.run
{% endhighlight %}

### Let's start defining the application

Something has changed from last application we built.
Our logic is becoming more and more complicated, we need organization.

We created a class named **Application** that inherits from Gtk::Application.

At the end of the scritp you can see that we are going to instantiate that class and run it.

All windgets we are going to use are going to become attributes of this class.

### Initializing Box container

Tree simple steps are needed in order to utilize a Box container:

* we need to initialize it
* we need to define his direction (:horizontal or :vertical) 
* we need to add it to the window

{% highlight ruby %}
box = Gtk::Box.new :horizontal # it could be :vertical too
window.add box
{% endhighlight %}

Once we have done that we can start adding widgets to it.

### Adding widgets to the box

Adding widgets to a Box is pretty strait forward:

* initialize the widget
* **add** the wiget to the box

{% highlight ruby %}
@hello_button = Gtk::Button.new :label => "Hello"
box.add @hello_button

@world_button = Gtk::Button.new :label => "World"
box.add @world_button

@label = Gtk::Label.new 'Still empty!'
box.add @label
{% endhighlight %}

I decided to initialize the widget as Application class attributes in order to be able to utilize them in 
the following methods.

### Events events.. events

We need to handle the events in order to control the behaviour of the application.
I this case I linked the signal **clicked** to the **Application** method call **on_btn_clicked**.

{% highlight ruby %}
@hello_button.signal_connect "clicked" do |sender, event| 
  on_btn_clicked sender, event
end

@world_button.signal_connect "clicked" do |sender, event| 
  on_btn_clicked sender, event
end
{% endhighlight %}

This method take the sender label (label contained in the button) and set the @label text accordingly.

{% highlight ruby %}
def on_btn_clicked sender, event
  @label.text= sender.label
  puts "clicking: " + sender.label
end
{% endhighlight %}

### Conclusions

Things are becomeming more interesting now.
We are able to mix some widget and some behaviour in a functioning App.

See you next time.
