---
title: "Space Game — Session 3"
date: 2017-02-05 10:00
grade: primary
published: true
---

# Space Game — Session 3

So right now, you should have your perfectly working asteroid. It'll zoom past
the player, or bump into it for certain death.

Problem is, it's a bit boring if it just passes by and nothing else happens.

## "Fake" new asteroids

When the asteroid reaches the bottom, let's make a new one at the top!

Or even better, let's teleport the old asteroid to the top.

![](http://i.imgur.com/aUYLUTF.png)

That way to the player it looks like a new one!

## Check when the asteroid reaches the bottom

Right now, we have two behaviors:

1. `ship movement`
2. `asteroid movement`

We need to open one of these. __WHICH ONE?__

## STEP 1. Reset asteroid to top

What should happen, in plain English:

__ If the asteroid's Y coordinate is bigger than the height of the screen, set the asteroid's Y coordinate back to 0.__

1. Add a new "When Updating" event. You should know how to by now...

![](http://i.imgur.com/BFo3d8s.png)

2. Add an `if` block into the "When Updating" block.

Now let's have a look at the little triangle inside the `if`. Click on it to show a menu:

![](http://i.imgur.com/eEuUc2O.png)

3. Choose the `>=` block from one of the menus. __Can you find it?__
4. Now we have 2 blanks to fill in.
    - For the left one, go into the triangle menu and find `x of actor` and set it to `y of self`.
    - For the right one, we need to do the same but for the `screen height`
5. Add something that happens when the asteroid leaves the screen. Inside, the
   if block, let's __SET Y OF SELF TO 0__. Can you figure that out?
6. __TEST YOUR GAME__. The asteroid should reset to the top.

## STEP 2. The asteroid doesn't actually appear at the top!

True. It should fly in from the top!

Why is it? Look at the coordinates of this asteroid:

![](http://i.imgur.com/mtdiLFX.png)

See, the Y coordinate is at the top of the asteroid.

We need to actually put the asteroid at the Y coordinate a bit less than 0. How
much less? That depends on the __HEIGHT OF THE ASTEROID__.

Let's redo this:

1. Delete the 0 in `SET Y OF SELF TO 0`.
2. Click on the triangle menu and add a `negate` block. Can you find it?
3. Click on the triangle menu inside the `negate` and set it to `width of actor`. Can you find it?
4. Set `width of actor` to `height of self`.
5. __TEST YOUR GAME__

## STEP 3. More asteroids!

Pretty easy game so far. Maybe you can add more asteroids to make it more interesting!?

## STEP 4. Random X?!

Well now it's a bit boring. The asteroid just falls in one place.

How about, when you set the Y to `negate(height of self)`, maybe you can add an
extra block in there to `set x of self to (Random number between(0, screen
width))`? Can you figure that out?
