---
layout: post
title:  "Combobox"
date:   2020-09-02 12:00:00 +0200
categories: basics
tags: output combobox widget
---

![My first combobox](/rubygtkfun/images/posts/combobox.png){:class="aside-image"}

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

app = Gtk::Application.new("org.rubygtkfun.combobox", :flags_none)

def on_key_release sender, event
  puts sender.text
end

app.signal_connect "activate" do |application|
  window = Gtk::ApplicationWindow.new application
  window.set_title "My first window with a combo box"
  window.set_default_size 400, 100

  cb = Gtk::ComboBoxText.new
  cb.signal_connect "changed" do |w, e|
    on_changed w, e
  end

  cb.append_text 'Linux'
  cb.append_text 'Windows'
  cb.append_text 'Mac Os'

  window.add cb

  def on_changed sender, event
    puts sender.active_text
  end

  window.show_all
end

puts app.run

{% endhighlight %}

This code is minimal and it is there only to show how to instantiate a combobox and how to insert it in a window.

### Adding a combobox

{% highlight ruby %}
cb = Gtk::ComboBoxText.new
window.add cb
{% endhighlight %}

How you can see, in order to instantiate a **ComboBox**, I need to call the contructor of GTK ComboBoxText class.

Once I have done that I need to **add** this new **ComboBox** to the current window.

### Adding items to a combobox

The GTK ComboBoxText class has a method that allows to introduce items, the method is named **append_text**.
Items are importante because represents the set of possible choiches the user will be able to select.
Items can be strings like the following ones:

* Linux
* Windows
* Mac Os

Previously we defined the instance **cb**, that allows us to write:

{% highlight ruby %}
cb.append_text 'Linux'
cb.append_text 'Windows'
cb.append_text 'Mac Os'
{% endhighlight %}

### Getting the selected item from a combo box

Once the user selected an item from a combo box it is important to have access to that information in order to use it 
in the proceeding of the program.

The method **active_text** gives us access to that information.

We can use an assignment in order to store that information in a variable and use it later.

{% highlight ruby %}
myitem = cb.active_text
{% endhighlight %}


### 'changed' signal

Sometimes it is important to detect if the user changed his mind and made a new selection in the combo box.

It is possible for a Gtk ComboBox instance to trigger a signal named **changed**. 

We can intercept the signal as you see here:

{% highlight ruby %}
cb.signal_connect "changed" do |w, e|
  on_changed w, e
end
{% endhighlight %}



{% highlight ruby %}
def on_changed sender, event
  puts sender.active_text
end
{% endhighlight %}

### Conclusions







