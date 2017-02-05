---
title: "Enemy Health"
date: 2017-02-05 10:00
grade: secondary
---

# Enemy Health

## Add Enemy Health Script

### 1. Create a new js script

Create a new script and call it `EnemyHealth`.

### 2. Set up the necessary variables
```javascript
public var enemyHealth : int = 100;
```

### 3. Kill the enemy if its health is below zero
- Set up an `if statement` inside the `update` function 
- The condition should be: `enemyHealth` is smaller than 0.
  - (Remember the condition goes between `(` and `)`!)
- Inside the if statement, we add these two lines:
  - As always, make sure that you entered those lines after the `{` and before the `}` of the if statement.

```javascript
var animationTrigger : String = "Dead";
this.gameObject.collider.GetComponent(Animator).SetTrigger(animationTrigger);
```

## Adapt Shooting Script
Now we need to change the shooting script so that the enemies no longer die immediately when they are hit, but instead lose health.

### 1. Add a variable
Since the variable for each enemy's health is stored in the `EnemyHealth` script, we need a way to communicate between scripts. We do this by adding the `EnemyHealth` script in a variable:
```javascript
public var enemyHealth : EnemyHealth;
```

### 2. Update the update function
Instead of triggering the death animation, we now just want to decrease the hit enemy's health. 

To do this, we replace two commented-out lines (the grey one with the two slashes at the beginning) with the two lines underneath it:

```javascript
    //var animationTrigger : String = "Dead";
    //shootHit.collider.GetComponent(Animator).SetTrigger(animationTrigger);
    enemyHealth = shootHit.collider.GetComponent(EnemyHealth);
    enemyHealth.enemyHealth = enemyHealth.enemyHealth - 10;
```

The first one gets this specific enemy's current health from its specific `EnemyHealth` component. The second one reduces it by 10.

### 3. Test it!
how many times?


## I'm done! Oh no! What do I even do with myself now?! 

Feel free to add any of these features to your game:

- Adding a sound when the enemy is hurt
- Making the enemy sink through the floor when they die
- Showing each enemy's health above them
