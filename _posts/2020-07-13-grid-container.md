---
layout: post
title:  "Grid container"
date:   2020-07-13 12:00:00 +0200
categories: basics
tags: grid container
---

![Entry widget](/rubygtkfun/images/posts/grid.png){:class="aside-image"}

[Gtk.Grid](https://developer.gnome.org/gtk3/stable/GtkGrid.html) is a container which arranges its child widgets in something that behaves like a table.
This table is composed by rows and columns and it extends automatically to needed dimentions.

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
    super 'org.rubygtkfun.grid', Gio::ApplicationFlags::FLAGS_NONE

    signal_connect :activate do |application|
      window = Gtk::ApplicationWindow.new application
      window.set_default_size 300, 100
      window.set_title 'Example of a grid container'

      grid = Gtk::Grid.new
      grid.set_property "row-homogeneous", true
      grid.set_property "column-homogeneous", true
      window.add grid

      @hello_button = Gtk::Button.new :label => "Hello"
      grid.attach @hello_button, 0, 0, 1, 1 # child, left, top, width, height

      @world_button = Gtk::Button.new :label => "World"
      grid.attach @world_button, 1, 0, 1, 1 # child, left, top, width, height

      @label = Gtk::Label.new 'Still empty!'
      grid.attach @label, 0, 1, 2, 1        # child, left, top, width, height

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

### Initializing Grid container

The application we are building is simple. 
An instance of the grid container is created in the __initialize__ method and this instance is going to contain three buttons.

As usual, when we are working with a Grid container:

* we need to initialize it
* we need to set the necessary properties 
* we need to add it to the window

{% highlight ruby %}
      grid = Gtk::Grid.new
      grid.set_property "row-homogeneous", true
      grid.set_property "column-homogeneous", true
      window.add grid
{% endhighlight %}

For better understangind all properties you can use with [Gtk.Grid container](https://developer.gnome.org/gtk3/stable/GtkGrid.html) check out the documentation [page](https://developer.gnome.org/gtk3/stable/GtkGrid.html).

### Adding widgets to the grid

Children are added using the method **attach**. They can span multiple rows or columns. 
The Gtk.Grid.attach() method takes five parameters:

* The child parameter is the Gtk.Widget to add.
* left is the column number to attach the left side of child to.
* top indicates the row number to attach the top side of child to.
* width and height indicate the number of columns that the child will span, and the number of rows that the child will span, respectively.

{% highlight ruby %}
@hello_button = Gtk::Button.new :label => "Hello"
grid.attach @hello_button, 0, 0, 1, 1 # child, left, top, width, height
{% endhighlight %}

In this example we are creating a button having label "Hello" that is positioned in the grid at cohordinates (first top left cell)

* left: 0
* top: 0

and the cell has the following dimentions in terms of room taken in the grid

* width: 1
* height: 1
 
### Adding widgets to the grid: second way
     
It is also possible to add a child next to an existing child, using **attach_next_to**, which also takes five parameters:

* child is the Gtk.Widget to add, as above.
* sibling is an existing child widget of self (a Gtk.Grid instance) or None. The child widget will be placed next to sibling, or if sibling is None, at the beginning or end of the grid.
* side is a Gtk.PositionType indicating the side of sibling that child is positioned next to.
* width and height indicate the number of columns and rows the child widget will span, respectively.

### One more way to add widgets

Finally, Gtk.Grid can be used like a Gtk.Box by just using Gtk.Grid.add(), which will place children next to each other in the direction determined by the “orientation” property (defaults to Gtk.Orientation.HORIZONTAL).

### Conclusions

We have a new toy to play with. Using grid containers we could potentially create any kind of layout.

See you next time.
