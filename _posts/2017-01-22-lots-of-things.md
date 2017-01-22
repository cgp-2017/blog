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

### 1. Select your FPS controller

![](http://i.imgur.com/nZTUyh3.png)

### 2. Add a light component to it

![](http://i.imgur.com/G3rcsWU.png)

### 3. Disable and setup your light

![](http://i.imgur.com/JRyM9sL.png)

Couple of things here:

- The checkbox at the top should be off
- Set a color and intensity of your choice. There's no wrong answer here!

### 4. Light that gun up when you shoot!

- Easy peasy. Open up your `shoot` script.
- Add two new `private var`s:
  - `gunLight`. Its type is `Light` (__capital L__)
  - `turnOffLight`. Its type is `float`
- In your `Start` function, there's the line `gunAudio = GetComponent(AudioSource);`.
  - Add another line inside the `Start` function , but this time for the `gunLight`. Think you can figure out how to do it? What's the component called?
- Enable the light when you __shoot__.
  - The line is `gunLight.enabled = true;`
  - __You need to figure out which function to put this in__


### 5. Try it out

So what happens?

The light goes on but never goes off. This is where we make one more adjustment

### 6. `turnOffLight` timer

- Right after the `Shoot()` function is called when you click the mouse, there's this line:

```
nextShot = Time.time + cooldown;
```

- Add a new line below this one. We're gonna do the same for `turnOffLight`. We're gonna set its value to be `Time.time + 0.1`


### 7. Turn off the light after a while

Update method looks like this for now:

```
function Update () {
  if (Input.GetButton("Fire1") && Time.time > nextShot) {
  	gunLight.enabled = true;
    Shoot();
    nextShot = Time.time + cooldown;
    turnOffLight = Time.time + 0.1f;
  }
}
```

Let's add 3 more lines __below the if statement__ to make it look like this:


```
if(Time.time >= turnOffLight) {
  gunLight.enabled = false;
}
```

This will turn off the light if now enough time has passed.


### 8. TRY IT
