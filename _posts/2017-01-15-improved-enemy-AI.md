---
title: "Improved Enemy AI"
date: 2017-01-15 10:00
grade: secondary
published: true
---

# Improved Enemy AI

## Let's make sure we're all on the same page

### What you should have set up in your game before starting on this task:
- the follow.js script
- at least one enemy type
  - with the follow.js script attached

### What we are about to add to the AI programmed in the follow.js script:

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
<summary><b>Try it and then check your answer by clicking on the black triangle!</b> </summary>
  <pre><code>
      function MoveTowards(target) {

      }
  </code></pre>
</details>



Now we take the the code from last week and move it from the `Update` function to our new `MoveTowards` functions. We replace `player.position` with `target`.
Why? Because `target` is the parameter of our `MoveTowards` function. When we use the function we put the location we want to move to inside the brackets:

```javascript
MoveTowards(overThere);
```
(this will work as long as 'overThere' is a position that Unity understands.)

A parameter is just a special term for variables you give to a function to do with what it's supposed to do.

For example, you might have a function called `Add(a,b)` that takes two numbers as parameters (a and b), adds them together and then returns the result.

So `Add(1,2)` would return `3`.

For our `MoveTowards(target)` function, the parameter needs to be a postion.

<details>
<summary><b>How should it all look put together? </b></summary>
 <pre><code style="javascript">
function MoveTowards (target) {
  var animationName : String = "Death";
  if( !GetComponent(Animator).GetCurrentAnimatorStateInfo(0).IsName(animationName)) {
    nav.SetDestination (target);
  }
}
</code></pre>
</details>


## Random Walking
Let's write another function. This time it will be called "RandomMovement" and will tell the AI how we want it to move randomly. It won't have a parameter.

<details>
<summary><b>Try setting it up</b></summary>
 <pre><code style="javascript">
  function RandomMovement () {

  }
</code></pre>
</details>


Let's move on to the content of our function. We want our enemy to move in random directions. But how do we express this so that a computer understands this? Let's break it down!
- the enemy should pick a random direction
- then it will move there for a certain amount of time
- and then it should pick a new direction
- ..... and so on

First thing we notice: We need to keep track of how long the enemy has been moving in one direction!

How do we do this?

We add a new variable!
- name "duration"
- type float-point number
- initial value: 0
- we won't need to see or modify the variable in Unity

<details>
<summary><b>Add it to the other variables at the top of the script!</b> </summary>
 <pre><code>
  private var duration : float = 0;
</code></pre>
</details>

So let's say we want to pick a new random direction every 10 seconds. How can we implement that?

- we start at 0 seconds
  - random direction should be picked
- now 10 seconds pass
  - the direction shouldn't change
  - duration should be updated to how much time as passed
- after 10 seconds
  - the duration should be reset


You might already have realised that we will need an `if` statement to make that happen.

<details>
  <summary><b>Try writing it! (Don't worry about how to pick the direction--just the if statement structure)</b> </summary>
 <pre><code>
  if (duration == 0) {  
    // here we will put the code to pick a random direction (THIS IS JUST A COMMENT)
    duration = Time.deltaTime;
  } else if (duration > 10) {
    duration = 0;
  } else {
    duration = duration + Time.deltaTime;
  }
}
</code></pre>
</details>


How do pick a random positon to move towards in Unity?

We start with our current position

<details>
<summary><b>What is our starting point? (Remember this is the direction the enemy should go.)</b></summary>
  the enemy's current position!
</details>

<details>
<summary><b>How do we get that in Unity?</b></summary>
  <code>this.gameObject.transform.position</code>
</details>


We use a command called `Random.onUnitSphere`. Think of it as a bubble. It's exactly one unit in diameter. By adding it to our characters current position, we make it a bubble that surrounds the enemy.
This command picks one random point on this bubble -- so you can get any possible direction the enemy could be moving towards.
But one unit is not very far. How do we fix this? We just multiply it by a higher number! 50 should be fine.

To sum up, every time the duration is 0, we want the enemy to move towards its position plus a random point on the sphere times 50.

<details>
<summary><b>Translated into javascript it looks like this: </b></summary>
 <pre><code>
    MoveTowards(this.gameObject.transform.position + Random.onUnitSphere * 50);
</code></pre>
</details>

Hopefully, you realized where in our function that last line should go. Double-check below:

<details>
<summary><b>How should the completed function look? </b></summary>
 <pre><code>
  function RandomMovement ()
{
  if (duration == 0) {
    MoveTowards(this.gameObject.transform.position + Random.onUnitSphere * 50);
    duration = Time.deltaTime;
  } else if (duration > 10) {
    duration = 0;
  } else {
    duration = duration + Time.deltaTime;
  }
}
</code></pre>
</details>

## If statement logic

Now we put this all together by writing some if-statement logic in the update function:


Let's recap! How should this AI work?

We want to have a couple variables that define the enemy's behaviour:

- is it chasing you?
  - --> variable name "following", possible values: true/false
- if it is chasing you, does it always know where you are or does it have a range?
  - --> variable name "hasRange", possible values: true/false
- if it has a range, how big is it?
  - --> variable name "range", possible values: numbers
- if it isn't following you or if you are out of range, is it walking around?
  - --> variable name "idleWalking", possible values: true/false


Try putting these variables in javascript terms and adding them to the beginning of your script, so Unity can understand them too.
(Remember that the kind of variable that can only have true/false als values is called a "boolean" and that we want to be able to set up these variables for different enemies outside of the code!)

<details>
<summary><b>Q1: How would you write these variables? </b></summary>
<pre><code>
public var following : boolean;
public var hasRange : boolean;
public var range : int;
public var idleWalking : boolean;
</code></pre>
</details>

### How to get the distance

We know alreayd how to get the Position of the enemy and of the player.
<details>
<summary><b>Little reminder </b></summary>
<pre><code>
player.position
this.gameObject.transform.position
</code></pre>
</details>

But how can we get the distance between the two and then compare it to the range?

First we add a private variable called "distance" to the top of our script (it should be a type "Vector3").
<details>
<summary><b>Like this:</b></summary>
<pre><code>
private var distance : Vector3;
</code></pre>
</details>

To set it to the current distance between the two, we simply take enemy's position and subtract it from the player's position:
```javascript
distance = player.position - this.gameObject.transform.position;
```

How can we compare the distance (a vector) to the range (a number)?
```javascript
distance.magnitude < range
```
This will return *true* if you are in range and *false* if you are not.

### The actual if statement

Now let's structure our if statement. We have 3 possible behaviours.

- the enemy is chasing you
- it is moving randomly
- it is standing still


* **If** following is *true*
  * We want to check if the player is in *range*
  * **if** it is **OR** if the enemy has *no range*
    * we want to **MoveTowards** the *player*
  * **else** **if** idleWalking is *true*
    * we want to use **RandomMovement**
* (Otherwise the enemy will just not move -- no need to do anything here.)


So far, all our if statement condition looked like this:

```javascript
if(CONDITION) {
  //stuff that happens if condition is met
  }
```
But in the 3rd line, we want to check if **either** one **or** another condition is true. This syntax looks like that:

```javascript
if(CONDITION || SECOND_CONDITION) {
  //stuff that happens if either condition is met
  }
```

<details>
<summary><b>Try setting up the structure of this if statement:</b></summary>
<pre><code>
  if (following == true) {
    \\check if player is in range
    if (distance.mangnitude &lt; range || hasRange == false) {
      \\enemy follows the player
    }
  } else if (idleWalking == true) {
    \\enemy moves randomly
  }
}</code></pre>
</details>

Now as the last step, we just need to fill in the proper code for our place-holders:
- `distance = player.position - this.gameObject.transform.position;`
- `FollowPlayer();`
- `RandomMovement();`

Try it and then compare it with the completed function below:


<details>
<summary><b>The completed function should look like this:</b></summary>
<pre><code>function Update ()
{
  if (following == true) {
    distance = player.position - this.gameObject.transform.position;
    if (distance.magnitude &lt; range || hasRange == false) {
      FollowPlayer();
    }
  } else if (idleWalking == true) {
    RandomMovement();
  }
}</code></pre>
</details>
