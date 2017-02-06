---
title: "Lots of things"
date: 2017-01-15 10:00
grade: secondary
published: true
---


# Lots of things you can do

You'll find here lots of small things you can add to your game:

1. Giving Ethan a little color
2. Ammo for your gun and ammo to pick up
3. Add a little flash to your gun
3. Build and play your game

## PS: IF YOU EVER LOSE THEM, YOUR SCRIPTS ARE [HERE](https://cgp-2017.github.io/blog/2017/01/22/scripts.html)

## Giving Ethan a little color

Okay, this one has been asked for a lot.

First off, right click and save this picture:

![](http://i.imgur.com/P7wsEuI.jpg)

Yes. I know. Horrifying. This is how textures work.

Applying this on Ethan is __super easy__.

### 1. Add the texture to Unity

Drag the picture with the horrors in the `Textures` folder.

![](http://i.imgur.com/APYSj4I.png)

### 2. Open up Ethan's body

![](http://i.imgur.com/MYZ8Rul.png)

### 3. Expand his materials section

![](http://i.imgur.com/cZUBAJa.png)

Now, click on the little circle next to Albedo, and select your texture that you dragged in.

### 4. DONE. TRY IT

## Ammo for your gun and ammo to pick up

The concept is simple.

You start with a certain amount of ammo, and when you shoot, you lose one bullet. When you have no more bullets, you can't shoot.

Let's open up our shooting script.

### 1. One new public var

- Add a new `public var`:
  - `ammo`. Its type is `int`, with a value of 100.

### 2. Subtract one piece of ammo

We need to add __one line of code__ to the `Shoot` function. Just make it reduce the value of `ammo` by one

__You need to figure that one out!__


### 3. Don't shoot if there's no ammo

One more piece of code to get this working. Look at the first `if` statement in the `Update` method: `if (Input.GetButton("Fire1") && Time.time > nextShot) {`.

Let's add another `&&` part:

```
if (Input.GetButton("Fire1") && Time.time > nextShot && ) {
```

__Now you need to write in code: Ammo is bigger than.... Bigger than what?__


### 4. Ammo boxes

I'll just leave this here:

![](http://i.imgur.com/ypFGvhk.png)

### 5. COLLECT them 😉

Maybe there's a COLLECTING script you can copy from?

What tag should we make for our AMMO boxes?

What should happen to our AMMO value when you pick up a box?

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

## Build and play your game

- Click on `File > Build Settings`.
    - Make sure that __only the scenes you made__ are ticked. Click on `Build` at the bottom of the window.
- Choose a destination.

That's it!
