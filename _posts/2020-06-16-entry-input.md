---
layout: post
title:  "Entry widget and input"
date:   2020-06-16 12:00:00 +0200
categories: basics
tags: input entry
---

![Entry widget](/rubygtkfun/images/posts/entry.png){:class="aside-image"}

The Entry widget allows the user to input an information. It appears in the shape of a box where te user can click in order to write some text or a number.

In the image you see aside the **Entry widget** is as big as the containing window so it is difficult to see his shape.

Let's see an example together.

{% highlight ruby %}
#!/usr/bin/ruby

require 'gtk3'

app = Gtk::Application.new("org.rubygtkfun.entry", :flags_none)

def on_key_release sender, event
  puts sender.text
end

app.signal_connect "activate" do |application|
  window = Gtk::ApplicationWindow.new application
  window.set_title "My first window with a label"
  window.set_default_size 400, 400

  entry = Gtk::Entry.new
  window.add entry

  entry.signal_connect "key-release-event" do |w, e|
    on_key_release w, e
  end

  window.show_all
end
puts app.run
{% endhighlight %}

### Adding an Entry widget

In order to add an etry widget we need to initialize it and then we need to add it to the containing window. 

{% highlight ruby %}
entry = Gtk::Entry.new
window.add entry
{% endhighlight %}

That is more or less it for now, we are going to see how to create a logic and a nice to see positioning of widgets in a window in some next article.

### Getting information from an Entry Widget

How can you get the text that is contained in an entry widget?

{% highlight ruby %}
entry = Gtk::Entry.new
window.add entry
puts entry.text
{% endhighlight %}

The **text** method will help you with that.

The last line of code gets the text contained in the entry widget and print it on the console.

### Setting text of an entry widget

Setting the text of an entry widget is as easy as writing **entry.text= 'my new text'**
The API of gtk3 is really well designed and easy to use.

Be careful, the setting method is called **text=** so if you are trying to write **entry.text = 'my new text'** you are going to receive an error message

### Connecting signals

{% highlight ruby %}
entry.signal_connect "key-release-event" do |w, e|
  on_key_release w, e
end
{% endhighlight %}

We said in the first post that gtk3 programming is all about connecting events to functions or methods. The two lines of code you see above are there to intercept the event **key-release-event** and call the function named **on_key_release** and defined at the very start of the code.

This function just write (puts) the text contained in the widget, an entry in this case, that sent the signal.

{% highlight ruby %}
def on_key_release sender, event
  puts sender.text
end
{% endhighlight %}

In the image aside you can see that I was typing some text and that method was called every time I released a button of my keyboard. You can see the text increasing as I was typing.

### Conclusions

We can input information and output information, next step will be about how to use a button.

The code I have written is avaiable [on github](https://github.com/fabiomattei/rubygtkfun-code).

