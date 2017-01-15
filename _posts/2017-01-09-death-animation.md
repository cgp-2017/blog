---
title: "Death Animation"
date: 2017-01-15 10:00
grade: secondary
---

# __Death Animation__

# Animation Controllers

Last time, we added some new assets to our game from the Unity demo. We'll be using some of these to make things a little more interesting.

If you haven't already, add a Zombunny to your game's Hierarchy.

Click on the Zombunny and check it out in the Inspector on the right.

![Zombunny](http://i.imgur.com/A4eId65.png)


What we're interested in is the "Animator" section. Particularly, the Controller. Here we can see that the controller is an "EnemyAnimatorController".

This is something we imported from the demo, and we can have a look at it. Go into the Project view, open the \_CompletedAssets folder, and inside that open the Animation folder.

![Animator view](http://i.imgur.com/DPSALl1.png)

Here you'll find the different objects for animation. Let's double click on the EnemyAnimatorController.

# The Animator View

Don't worry! The Scene editing view isn't gone. You can see it's now changed into the Animator tab.

Let's go over what we see here:

![Inspector view](http://i.imgur.com/SiyF883.png)

We see 5 boxes here:

- Any State
- Entry
- Idle
- Death
- Move

These 5 boxes represent `states`. This means that there are 5 states of animation. The character can either be in "Any State", "Entry", "Idle" (not moving), "Death", or "Move".

You're probably wondering what the arrows between states mean. These are transitions. That is, changes between states.

Let's look at these in detail:

1. The enemy can go from `Any State` to `Death`. Makes sense, right? No matter what the enemy is doing, it can die at any time.
2. The enemy can go from `Move` to `Idle`. The enemy can be either moving or not moving. Right.
3. `Entry` to `Move`. Okay, this one is a little more special.

See, `Entry` is a bit of a special state. It's the state that you start with. That means that you need to give the Entry state something to move to. This is why our default state is the `Move` one. You'll notice this when you start the game. The enemy starts moving right away.

If you didn't guess this already, `Any State` represents all states.

You might be wondering: How do we tell enemies to switch between states? What we need to do is `trigger` the transitions. Once again, the transitions are represented by the arrows between states.

Let's click on the arrow between `Any State` and `Death`.

You'll notice the inspector view changed on the right.

![Transition Inspector](http://i.imgur.com/ItKgFGc.png)

There's quite a lot going on here. The biggest part you might notice is the timing of switching between animations.

What we're interested in here is the `Conditions`. Here, the demo already gave us a contiditon for switching to the `Death` state. In order to do so, in our code, we need to trigger the `Dead` condition (notice the capital D!)

# So what are we doing today, then?

What indeed:

1. When we shoot an enemy, we'll trigger the death animation.
2. When the enemy is in the death animation, it will not move (duh! Corpses don't move)

# 1. Trigger the death animation

Let's open up our list of scripts. I hope by now I don't need to tell you which one we should be looking at. 🙃

In the script, let's look at the part we've been working with over the last few weeks:

```
  if(Physics.Raycast(shootRay, shootHit, range)) {
    if(shootHit.collider.tag == "Enemy") {
      Destroy(shootHit.collider.gameObject);
    }
  }
```

Here, when we shoot an object, if it has the "Enemy" tag, then it gets destroyed.

Let's replace the line `Destroy(shootHit.collider.gameObject);` with these two:

```
  var animationTrigger : String = "THIS IS THE WRONG VALUE";
  shootHit.collider.GetComponent(Animator).SetTrigger(animationTrigger);
```

In the first line, we defined a variable called animationTrigger. Its type is String. If you didn't already know, a String is a "String" of characters between quote marks. That is, you can have anything like "hi mom" or "12345" and it will be a string, so long as it has the quote marks. We've already made the value be "THIS IS THE WRONG VALUE".

The second line is a bit more complex. We go into the shootHit's collider, like we did for getting its tag, then get its Animator component (Remember the first step we took we looked at the Zombunny's components? It had an Animator component), and we set a trigger on it. What trigger? Why, the name of the Condition to trigger the Death animation.

If you have a keen eye, you'll notice that the value "THIS IS THE WRONG VALUE" is, as suggested, the wrong value.

My question to you, dear reader is this: What should we set the value to be? Remember, we saw the Condition earlier. HINT HINT.

Once you've entered the correct trigger to kill the enemy, you're done. Test it!

But be warned: This will only work on the Zombunny, the Zombear and the Hellephant. If you're trying this on Ethan or a cube, you're out of luck. They don't have a Death animation.

Moving on!

# 2. Stop moving after death.

So you'll notice that if you shoot the enemy and it falls over dead, it keeps moving toward you. I don't need to tell you how creepy this is. One thing is a moving living dead, but a dead moving living dead? NOPE

So anyway. Let's look at the script where the enemy `follow`s you. You know which one, right?

In particular, let's look at the `Update` method:

```
  function Update ()
  {
     nav.SetDestination (player.position);
  }
```

Looks good. Except the enemy should ONLY be moving if it's not dead. Making the change will require an if statement wrapped around the movement line `nav.SetDestination (player.position);`:

Let's have a look:


```
  function Update ()
  {
    var animationName : String = "ONCE AGAIN THIS IS THE WRONG VALUE";
    if( !GetComponent(Animator).GetCurrentAnimatorStateInfo(0).IsName(animationName)) {
       nav.SetDestination (player.position);
    }
  }
```

Let's go through the lines again:

First, like before, we define a String variable, this time called animationName.

The next line is more interesting and complex.

You may notice the exclamation mark `!`. This stands for NOT. This means that if the next statement is false, then we run the code. Sounds confusing, right? Here's a simpler example:

```
  !(1 + 1 == 2) //=> This is false, because 1 + 1 IS equals 2
  !("hello" == "goodbye") //=> This is true, because the two strings are NOT equal
```

Let's go on with that line. We get this object's (the enemy's) Animator object, and get its state info, and check if its name is `animationName`. It sounds a little confusing, but what it means in plain English is as follows:

If this object's animator's current state does NOT have the name "ONCE AGAIN THIS IS THE WRONG VALUE", then the object will move.

Naturally, "ONCE AGAIN THIS IS THE WRONG VALUE" is not correct. What we should do is have the correct animation name for when the enemy has died.

Hmm... What was it called again? Surely you can look again at the Animator view and see the name. Remember to get the capitalization right.

Done? Good, now go test it.

But hey. After it falls it keeps moving. Right?

RIGHT?!

Give it a second. What's actually going on is that the corpse slides a little until it runs out of momentum. Ever play Portal? Then you know what momentum is.

When you slide, you have some speed already but you'll keep going until you've rubbed against the ground enough and come to a full stop.

In this situation, it makes sense for a monster to slide on the floor a little with all that speed it was running at you with.

# But hey okay, I'm a super genius and I'm done. What now?

It's important not to overload you. Play around with these new things! Try changing the animations. Make tricky enemy placements. Import stuff from the asset store like obstacles and see what works and what doesn't!
