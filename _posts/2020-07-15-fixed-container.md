---
layout: post
title:  "Fixed container"
date:   2020-07-15 12:00:00 +0200
categories: basics
tags: fixed container
---

![Entry widget](/rubygtkfun/images/posts/fixed.png){:class="aside-image"}

[Gtk.Fixed](https://developer.gnome.org/gtk3/stable/GtkFixed.html) is a container which allows you to position widgets at fixed coordinates.
To be more precise we can say that it allows you to place child widgets at fixed positions and with fixed sizes, given in pixels.

For most applications, you should not use this container! 

Using **GtkFixed** the user could experience: truncated text, overlapping widgets, and other display bugs.

{% highlight ruby %}
#!/usr/bin/env ruby

'''
This example demonstrates the Gtk::Grid container.

Author: Fabio Mattei
Website: https://fabiomattei.github.io/rubygtkfun
Last modified: July 2020
'''

require 'gtk3'

class Application < Gtk::Application

  def initialize
    super 'org.rubygtkfun.fixed', Gio::ApplicationFlags::FLAGS_NONE
	
	override_background_color :normal, Gdk::RGBA::new(0.2, 0.2, 0.2, 1)

    signal_connect :activate do |application|
      window = Gtk::ApplicationWindow.new application
      window.set_default_size 300, 150
      window.set_title 'Example of a grid container'

      @fixed = Gtk::Fixed.new
      window.add @fixed

      @hello_button = Gtk::Button.new :label => "Hello"
      @fixed.put @hello_button, 0, 0   # x, y

      @world_button = Gtk::Button.new :label => "World"
      @fixed.put @world_button, 100, 0 # x, y

      @label = Gtk::Label.new 'Still empty!'
      @fixed.put @label, 100, 100      # x, y

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
    @fixed.move @label, 200, 100
    @label.text= sender.label
    puts "clicking: " + sender.label
  end

end


app = Application.new

puts app.run
{% endhighlight %}

### Initializing Fixed container

As usual we use the initialize method in order create instances of a **Fixed** container, two buttons and a label.

As usual, when we are working with a Fixed container:

* we need to initialize it
* we need to add it to the window

{% highlight ruby %}
@fixed = Gtk::Fixed.new
window.add @fixed
{% endhighlight %}

This time I set the container as a class attribute using @fixed as variable name.
I did that in order to be able to use the **move** method later on.

### Adding widgets to the fixed container

Children are added using the method **put**.
The Gtk.Grid.attach() method takes tree parameters:

* The child parameter is the Gtk.Widget to add.
* x coordinate relative to top left container corner
* y coordinate relative to top left container corner

{% highlight ruby %}
@hello_button = Gtk::Button.new :label => "Hello"
@fixed.put @hello_button, 0, 0   # x, y
{% endhighlight %}
 
### Moving a widget
     
Is is possible to use the move method in order to move a widget already contained in the fixed container.

{% highlight ruby %}
def on_btn_clicked sender, event
  @fixed.move @label, 200, 100
  @label.text= sender.label
  puts "clicking: " + sender.label
end
{% endhighlight %}

We used the **on_btn_clicked** in order to make an example.
When the user hit a button, the lable widget moves to destination coordinates: x=200, x=100

### Conclusions

Fixed container should not be used but there are times when it comes out handy. 
Now we have this tool in our belt, is up to us to be wise about it.

See you next time.
