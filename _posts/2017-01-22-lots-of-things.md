---
title: "Lots of things"
date: 2017-01-15 10:00
grade: secondary
---

# Lots of things you can do

You'll find here lots of small things you can add to your game:

1. Giving Ethan a little color
2. Ammo for your gun and ammo to pick up
3. Add a little flash to your gun

## Giving Ethan a little color

## Ammo for your gun and ammo to pick up

## Add a little flash to your gun

Right now we have a sound when you shoot your gun, but it needs some visual feedback.

__Let's add a flash of light when you shoot__

1. Select your FPS controller

![](http://i.imgur.com/nZTUyh3.png)

2. Add a light component to it

![](http://i.imgur.com/G3rcsWU.png)

3. Disable and setup your light

![](http://i.imgur.com/JRyM9sL.png)

Couple of things here:

- The checkbox at the top should be off
- Set a color and intensity of your choice. There's no wrong answer here!

4. Light that gun up when you shoot!

- Easy peasy. Open up your `shoot` script.
- Add two new `private var`s:
  - `gunLight`. Its type is `Light` (__capital L__)
  - `turnOffLight`. Its type is `float`
- In your `Start` function, there's the line `gunAudio = GetComponent(AudioSource);`.
  - Add another line inside the `Start` function , but this time for the `gunLight`. Think you can figure out how to do it? What's the component called?


