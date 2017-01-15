---
title: "Improved Enemy AI"
date: 2017-01-15 10:00
grade: secondary
---

# Improved Enemy AI

## Let's make sure we're all on the same page

### What you should have set up in your game before starting on this task:
- the follow.js script
- at least one enemy type
  - with the follow.js script attached
  
### What we are about to add to the AI programmed in the follow.js script:
- random walking
- a set of if statements to customise the enemy behaviour with the following parameters
  - idle_walking?
  - is_following?
  - range?
  - speed(?)
  
### What's the result?
You will have a customisable enemy behaviour script you can add to different enemy types and then set up so they behave very differently from each other without changing the script itself:
- one enemy could always be following you
- another might walk around randomly and when you are close by start following you, until you out-run him again
- a third might simply be walking around and ignore you
- another could be standing completely still and then charge at you if you get too close

## Functions
A new concept we will be working with is defining our own functions. Up to now, we have just used the pre-definied Unity functions `function Update()` and `function Start()`.
Now we will start making our own functions.

To define a function you start by writing "`function`" its name (capitalized) and a set of "`()`". If your function will use a parameter (we'll explain what that is soon) you write its name inside the round brackets. Afterwards you put an open curly bracket "`{`", leave some empty lines for the content of the function and then close it with a closed curly bracket "`}`".

Try adding a function called "MoveTowards" to your `follow.js` script and give it the parameter "target".

<details>
  <summary>Try it and then check your answer by clicking on the black triangle! </summary>
  <code>
    function MoveTowards(target) {
    
    }
    </code>
</details>

## Random Walking

<details>
  <summary>How should it all look put together? </summary>
  ```
  function RandomMovement ()
{
  if (dauer == 0) {
  nav.SetDestination (this.gameObject.transform.position + Random.onUnitSphere * 20);
  dauer = Time.deltaTime;
  } else if (dauer > 5) {
  dauer = 0;
  } else {
  dauer = dauer + Time.deltaTime;
  }
}
```
</details>

## If statement logic


## Range
<details> 
  <summary>Q1: How would you write the other 3 variables? </summary>
   ```
public var hasRange : boolean;
public var range : int;
public var following : boolean;
public var idleWalking : boolean;
```
</details>

