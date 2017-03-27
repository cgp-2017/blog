---
title: "Jump Scare"
date: 2017-03-26 12:00
grade: secondary
published: true
---

# Jump Scare (Thanks, Larry!)

## STEP 1: Scare wall and enemy

Let's click on Create > Create Empty

We will in the next step make it a nice big wall that the player will collide with

Also add an enemy, move it slightly behind of the wall, so that it'll scare you!

## STEP 2: Components

1. Click on the empty object and look at the inspector
2. Rename it to "ScareWall"
3. Add a Box Trigger and make it a trigger
4. Add an Audio Source and disable "Play on Awake"
5. Change the transform so that it's a big wall

## STEP 3: New Script

Add a new Javascript and call it `JumpScare`.

In it, add the following variables:

- Public variable called `enemy` that's of type `GameObject`
- Public variable called `sound` that's of type `AudioClip`
- private variable called `screamAudio` that's of type `AudioSource`

Enter the following into the `Start` function:

```
  screamAudio = GetComponent(AudioSource);
  enemy.SetActive(false);
```

Finally, replace the `Update` function with the following:

```
function OnTriggerEnter (other : Collider) {

	if(other.tag == "THIS IS NOT CORRECT") {
  		screamAudiob.PlayOneShot(sound);
  		enemy.SetActive(true);
	}
}
```

You'll notice that the tag "THIS IS NOT CORRECT" is totally wrong. So what should the tag be? When WHAT collides with the scare wall?

## STEP 4: Attach all the things!

But you figure it out. What should we attach the script to? What should the sound and enemy values?

[Here's](http://soundbible.com/grab.php?id=1517&type=mp3) a sound I used, by the way:
