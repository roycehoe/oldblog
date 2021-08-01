---
layout: post
title:  "Hacky Holidays - Space Race: Unidentifi3d-Flying-Object"
tag: ["reverse engineering", "something"]
---

# Description
---

[Printer] - 30 points
The UFO was forged on one of the universe's most advanced printers - do you know which make and model? Enter the answer as `Make Model`.

[Layer by Layer] - 70 points
Do you know how GCode files work? Maybe you can find a hidden message along the layers. Flag format: CTF{answer}

---
# Introduction
---
Well, what do we have here? The file I am given is called `unidentifi3d.gcode`. But first, what even is a `.gcode`?

Phew, turns out that [it isn't some challenge-specific code](https://en.wikipedia.org/wiki/G-code); it is code used in [manufacturing](https://en.wikipedia.org/wiki/Computer-aided_manufacturing). An important snippet from [this article](https://howtomechatronics.com/tutorials/g-code-explained-list-of-most-important-g-code-commands/):

> The G-code commands instruct the machine where to move, how fast to move, and what path to follow.

Great! My first guess is that this `gcode` would "draw" out the flag for me.

---
# Solving the challenge: Part 1
---
After a little Googling, I found [this website](https://gcode.ws/) that can help read this code. Dumping the code in the website gave me this weird drawing:
![Unidentifi3d%20Flying%20Object%209005dd557a584ec9a532e1b7f72d94e7/Untitled.png](/images/Unidentifi3d-Flying-Object-images/pyramid.png)
At the bottom of the page, there are sliders. Sliding back and forth, I catch a glimpse of this:
![Unidentifi3d%20Flying%20Object%209005dd557a584ec9a532e1b7f72d94e7/Untitled%201.png](/images/Unidentifi3d-Flying-Object-images/flag.png)
I see the word `Flying_sau`. Lemme try `Flying_saucer`.

Oh, unexpectedly worked. Looks like this is the key for the second part of the challenge.

Flag: CTF{Flying_saucer}

Turns out, the sliders actually indicate layers of scaffolding. In simpler terms, 3D printers print objects by stacking layers upon layers till the object is created. One of the layers happened to be the flag. Now to solve the first part of the challenge.

---
# Solving the challenge: Part 2
---
The first challenge asks for the make and model. To summarise [this article](https://pediaa.com/difference-between-make-and-model/#:~:text=The%20main%20difference%20between%20make,about%20different%20types%20of%20products.):

- Make: Who is the manufacturer of the product? [Apple]
- Model: What is the product? [Iphone X]

Looking at the end of the `.gcode` file, I find this:

{% highlight gcode %}
;SETTING_3 {"global_quality": "[general]\\nversion = 4\\nname = Extra Fast #2\\n
;SETTING_3 definition = geeetech_A10M\\n\\n[metadata]\\ntype = quality_changes\\
;SETTING_3 nsetting_version = 16\\nquality_type = verydraft\\n\\n[values]\\nsupp
;SETTING_3 ort_enable = True\\n\\n", "extruder_quality": ["[general]\\nversion =
;SETTING_3  4\\nname = Extra Fast #2\\ndefinition = fdmprinter\\n\\n[metadata]\\
;SETTING_3 ntype = quality_changes\\nsetting_version = 16\\nposition = 0\\nquali
;SETTING_3 ty_type = verydraft\\n\\n[values]\\n\\n", "[general]\\nversion = 4\\n
;SETTING_3 name = Extra Fast #2\\ndefinition = fdmprinter\\n\\n[metadata]\\ntype
;SETTING_3  = quality_changes\\nsetting_version = 16\\nposition = 1\\nquality_ty
;SETTING_3 pe = verydraft\\n\\n[values]\\n\\n"]}
{% endhighlight %}

I have a hunch that this metadata contains the model which "manufactured" the flag. 

As it turns out, [geeetech A10M](https://www.google.com/search?q=geeetech+A10M&sxsrf=ALeKk02ISVd9VWKTdzgK3jVnd7WqGn-ZJA:1627394661107&source=lnms&tbm=isch&sa=X&ved=2ahUKEwiAqrzFtYPyAhXVZSsKHd2uAJIQ_AUoAXoECAEQAw&biw=956&bih=955) is the name of the model. 

Flag: geeetech A10M

---

Side note: This may be the first flag I have found that actually contains a space instead of an underscore

Another side note: I just want to acknowledge the little inside joke that the admins were trying to reference. Because who built the pyramids?

![Unidentifi3d%20Flying%20Object%209005dd557a584ec9a532e1b7f72d94e7/Untitled%202.png](/images/Unidentifi3d-Flying-Object-images/meme.png)
