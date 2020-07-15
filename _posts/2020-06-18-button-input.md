---
layout: post
title:  "Button widget and input"
date:   2020-06-18 12:00:00 +0200
categories: basics
tags: input button
---

![Entry widget](/rubygtkfun/images/posts/button.png){:class="aside-image"}

The Button widget allows the user to have a button in the interface he can push.

In the image you see aside the **Buttons widget** is as big as the containing window so it is difficult to see his shape. But if you push that button, some text appears in the console, this means that the button is there and the user can interact with it.

Let's see an example together.

{% highlight ruby %}
#!/usr/bin/env ruby

require 'gtk3'

app = Gtk::Application.new("org.rubygtkfun.button", :flags_none)

def on_btn_clicked sender, event
  puts "clicking: " + sender.label
end

app.signal_connect "activate" do |application|
  window = Gtk::ApplicationWindow.new application
  window.set_title "My first window with a button"
  window.set_default_size 400, 400

  button = Gtk::Button.new :label => "My new button"
  button.set_size_request 80, 30
  window.add button
        
  button.signal_connect "clicked" do |sender, event| 
    on_btn_clicked sender, event
  end

  window.show_all
end

puts app.run
{% endhighlight %}

### Adding a Button widget

In order to add a button widget we need to initialize it and then we need to add it to the containing window. When initializing a Button we need to give it some text, a label, that will drive the user to unrestand what the button is for.

{% highlight ruby %}
button = Gtk::Button.new :label => "My new button"
button.set_size_request 80, 30
window.add button
{% endhighlight %}

### Connecting signals

{% highlight ruby %}
button.signal_connect "clicked" do |sender, event| 
  on_btn_clicked sender, event
end
{% endhighlight %}

As we did in the past we need to describe the behaviour of the button using events. The two lines of code you see above are there to intercept the event **clicked** and call the function named **on_btn_clicked** and defined at the very start of the code.

This function just write (puts) the text contained in label of the button that sent the signal.

{% highlight ruby %}
def on_btn_clicked sender, event
  puts "clicking: " + sender.label
end
{% endhighlight %}

### Conclusions

Now we know how to create buttons, entry, labels. Next post will be about how to populate a window with many widgets.

The code I have written is avaiable [on github](https://github.com/fabiomattei/rubygtkfun-code).

See you next time
