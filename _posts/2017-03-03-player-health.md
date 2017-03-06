---
title: "Player Health"
date: 2017-03-05 12:00
grade: secondary
published: true
---

# Player Health

Now let's have some health for our player.


## STEP 1: Create an instance of the health bar

We'll have our own instance of the health bar prefab we made a few weeks ago. Drag it into the canvas:

![](http://i.imgur.com/RrMPDgW.png)

MAKE SURE IT'S INSIDE THE CANVAS

## STEP 2: Make sure the health bar is visible in the screen

![](http://i.imgur.com/vmjsiij.png)

- Move the X and Y position so that the health bar is visible in the game view.
- Make sure the health bar is anchored to the top left. You've done this before.

__RUN THE GAME__. It should show the health bar, but NOT DECREASE IT. We'll do that now.

## STEP 3: Overhaul of the `damage` script

Right now, when an enemy touches the player, the game is over and we start again.

Now, we'll add a health bar.

Open your `damage` script.

Add the following variables to the top:

- Public variable called `health` that's of type `int` and initial value of 100.
- Private variable called `maxHealth` that's of type `int`.
- Public variable called `healthPanel` that's of type `GameObject`.
- Private variable called `healthSlider` that's of type `UnityEngine.UI.Slider`.

## STEP 4: Setup the values

In the `Start` function, add the following two lines:

```
maxHealth = health;
healthSlider = healthPanel.GetComponentInChildren(UnityEngine.UI.Slider);
```

## STEP 5: Update the health bar and kill the player

In the `Update` function, make sure the content is as follows:

```
	if (health <= 0) {
      // WHAT SHOULD HAPPEN HERE?
	}
	healthSlider.value = parseFloat(health)/parseFloat(maxHealth);
```

You'll notice I left a comment in there. What __SHOULD__ happen when the player reaches zero health? (HINT: Maybe look around in this script?)

## STEP 6: Knock off some health

In the `OnTriggerEnter` function, delete the lines and add the following:

```
	if(other.tag == "enemy") {
      // WHAT SHOULD HAPPEN HERE?
	}
```

Again with the comments! Here, your health should go down, but by how much? You figure it out!

## STEP 7: Wire it all up

On the FPS controller, you should already have the damage script attached. Make sure to add that health bar! I won't tell you what to do ;).

![](http://i.imgur.com/PCovOTm.png)
