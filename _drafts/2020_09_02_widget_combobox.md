---
layout: post
title:  "Combobox"
date:   2020-09-02 12:00:00 +0200
categories: basics
tags: output combobox widget
---

![My first combobox](/rubygtkfun/images/posts/label.png){:class="aside-image"}

Nothing is better of a combobox to allow the user to choose an option between a set of possible values!

Let's start from the beginning.

Imagine you are building an application where the user has select the operating system he is currently using.
There is a finite set off possible values the user can select:

* Linux
* Windows
* Mac Os

That is a typical case of choosing between a selection.

There is a number of ways we can ask this information to a user in a software interface, one of the most effective ways is using 
a combo box.

Let's check some code out.

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

Writing two lines of code we added a label to the window.
You can see it in the center of the window, it has some text as content: "My brand new label"

The first line of code creates an instance of a Label widget and set its text to "My brand new label".

The second line of code add the label to the window.

### Setting text of an already created label

What can you do if you want to set the text of a label that is already being instantiated before?

{% highlight ruby %}
label = Gtk::Label.new 'My brand new label'
window.add label
label.text= 'Hello world'
{% endhighlight %}

You can use the method **text=** and you can set the text as you wish.

### Getting text from a table

How can you get the text that is contained in a label?

{% highlight ruby %}
label = Gtk::Label.new 'My brand new label'
window.add label
puts label.text
{% endhighlight %}

The **text** method will help you with that.

The last line of code gets the text contained in the label and print it on the console.

### Conclusions

Many things can be said about the label, our exploration just started.
If you give the command **puts label.methods**:

{% highlight ruby %}
label = Gtk::Label.new 'My brand new label'
puts label.methods
{% endhighlight %}

You'll find there is a plethora of methods this widget can use to perform many tasks.
We just scratched the surface.

See you next time!
