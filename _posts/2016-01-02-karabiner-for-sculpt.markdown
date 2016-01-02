---
date: 2016-01-02 12:19:44
modified:
layout: post
comments: true
title: "Microsoft Sculpt Key Remapping for Mac OS X Yosemite 10.11.2"
slug:
summary:
categories:
  - technology
tags: 
  - keyboard
  - osx
link: 
tweet: Use the Microsoft Sculpt on OS X 10.11.2 and tired of remapping keys?

---

I use the Microsoft Sculpt ergonomic keyboard. Since it's made by Microsoft, it has keys laid out for Windows. Left of the spacebar you have Alt, Windows, and Control, whereas a typical Mac user would expect Command, Option, Control. The names don't match, nor does the functionality.

To reset the keys to work using typical Mac keyboard muscle memory, one would go into System Preferences -> Keyboard -> Modifier Keys -> Microsoft 2.4Ghz Transeiver vX.0 and swap Command and Option.

However, when Apple updated OS X to 10.11.2 they broke the keyboard modifier key settings in System Preferences. They no longer persist between sessions. If I unplug the transeiver, the keys are reset.

I did my duty and [filed a radar](http://www.openradar.me/radar?id=5065483791368192), please go and submit a similar one if you're running into this issue as well.

I got tired of resetting it each time I plugged my Mac into my display with the transeiver plugged into it. So I used Karabiner, a great tool for key remapping, to swap the two.

If you're in a similar situation, here's how you do it:

1. Download and install [Karabiner](https://pqrs.org/osx/karabiner/). It works on a low level, and will ask you for potentially scary permissions. But it's a pretty commonly used tool, well supported, and well regarded by Mac power users.

2. Open the 'private.xml' file to enter your custom key remapping. You can find the 'private.xml' file by choosing the Misc & Uninstall tab.

3. Add the keyboard definition and the two items included below. Your entire file should look similar to:

{% highlight xml %}
<?xml version="1.0"?>
<root>

<devicevendordef>
    <vendorname>Microsoft</vendorname>
    <vendorid>0x045e</vendorid>
</devicevendordef>

<deviceproductdef>
    <productname>Sculpt</productname>
    <productid>0x07a5</productid>
</deviceproductdef>

<item>
    <name>Remap Sculpt Alt to Command</name>
    <appendix>This maps the Microsoft Sculpt's ALT Key to Command.</appendix>

    <identifier>sculpt.alt_to_command</identifier>
    
    <device_only>DeviceVendor::Microsoft,
    DeviceProduct::Sculpt</device_only>

    <autogen>
        --KeyToKey--
        KeyCode::OPTION_L,

        KeyCode::COMMAND_L
    </autogen>
    <autogen>
        --KeyToKey--
        KeyCode::OPTION_R,

        KeyCode::COMMAND_R
    </autogen>
</item>
<item>
    <name>Remap Sculpt Windows to Option</name>
    <appendix>This maps the Microsoft Sculpt's Windows Key to Option.</appendix>

    <identifier>sculpt.windows_to_option</identifier>

    <device_only>DeviceVendor::Microsoft,
    DeviceProduct::Sculpt</device_only>

    <autogen>
        --KeyToKey--
        KeyCode::COMMAND_L,

        KeyCode::OPTION_L
    </autogen>
    <autogen>
        --KeyToKey--
        KeyCode::COMMAND_R,

        KeyCode::OPTION_R
    </autogen>
</item>
</root>
{% endhighlight %}

4. Open Karabiner again to the main 'Change Key' tab and tap 'Reload XML', you will now be presented with two options at the top (the two items we just added to Karabiner's options). 

5. Enable both options, go and test that it works

6. Move on happily knowing that you won't have to wait for Apple to release an update to fix this obscure bug