---
title: "Second Weapon"
date: 2017-03-05 12:00
grade: secondary
published: true
---

# Second Weapon

In this session, you'll add a second gun to your arsenal. If you finish, you'll be able to add more weapons easily.

## STEP 1: Find a new gun.

Grab a new gun from the Asset Store. You can open the asset store from the "Window" menu at the top of the screen.

![](http://i.imgur.com/tDauNTG.png)

I went with the shotgun 🔫

Remember to import it.

## STEP 2: Add a new sound for your second gun

Download a free sound for your gun. I went with a shotgun sound:

http://soundbible.com/grab.php?id=2095&type=mp3

## STEP 3: Place the gun on your player

Open up your `FirstPersonCharacter` inside your `FPSController` and add the gun next to your other one:

![](http://i.imgur.com/ScDi99t.png)

## STEP 4: Gun Position

Rotate the new gun so it looks like you're holding it.

Looks kinda weird with both there, though....

## STEP 5: Hide the new gun

Select the new gun, and in the inspector, disable your new gun.

## STEP 6: New shooting logic

Now we step into the code. Open up your `shoot` sript and add the following new variables at the top:

- Public variable called `damage1` that's of type `int` and initial value of 10.
- Public variable called `damage2` that's of type `int` and initial value of 50.
- Public variable called `cooldown2` that's of type `float` and initial value of 2.0.
- Private variable called `currentWeapon` that's of type `int` and initial value of 1.
- Private variable called `pew2` that's of type `AudioClip`.
- Private variable called `gun1` that's of type `GameObject`.
- Private variable called `gun2` that's of type `GameObject`.

## STEP 7: Actual weapon switching

Inside your `Update` function, before any `if` statements, add these lines.

```
  if (Input.GetKeyDown ("1")) {
  	currentWeapon = 1;
  	gun1.SetActive(true);
  	gun2.SetActive(false);
  }

  if (Input.GetKeyDown ("2")) {
  	currentWeapon = 2;
  	gun2.SetActive(true);
  	gun1.SetActive(false);
  }
```

__TRY RUNNING YOUR GAME__. The guns should now switch!

## STEP 8: New sound

So now, in your `Shoot` function, you have this line: `gunAudio.PlayOneShot(pew);`

Replace that with these lines:

```
	if (currentWeapon == 1) {
  		gunAudio.PlayOneShot(pew);
	}
	if (currentWeapon == 2) {
  		gunAudio.PlayOneShot(pew2);
	}
```

__TRY RUNNING YOUR GAME__. The guns should now sound different.

## STEP 9: Different cooldowns:

Now let's have different cooldowns for our guns.

In your `Update` method you have this line: `nextShot = Time.time + cooldown;`.

Replace it with these ones:

```
    if (currentWeapon == 1) {
    	nextShot = Time.time + cooldown;
    }
    if (currentWeapon == 2) {
    	nextShot = Time.time + cooldown2;
    }
```

__TRY RUNNING YOUR GAME__. The guns should now react differently.


## STEP 10: Different damages

Okay, so until now we've been copy pasting nicely.

Your `Shoot` function should have the following line: `enemyHealth.enemyHealth = enemyHealth.enemyHealth - 10;`

All well and good. But now change it so that `IF` your current weapon is the 1st one, to take away `damage1` health from the enemy, and add another one where `IF` the current weapon is the second one, to take away `damage2` health.

__TRY RUNNING YOUR GAME__. The guns should now do different damage.

## STEP 11 (Optional): Add a third gun.

Feeling up to the challenge? Add a third gun. Should need a few more variables and `if` statements.
