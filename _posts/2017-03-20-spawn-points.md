---
title: "Spawn Points"
date: 2017-03-20 12:00
grade: secondary
published: true
---

# Spawn Points

Let's add a random element to our game. Enemies will now spawn at specific points instead of being set by us.

## STEP 1: Create a prefab for every enemy type

Drag the enemy you want to make a prefab of from the scene hierarchy into the `prefabs` folder.

When you do, open it up in the inspector and make sure that:

- The canvas is set to none
- The healthbar prefab is set

![](http://i.imgur.com/bLzCkUP.png)

## STEP 2: Create and position spawn point

In the hierarchy, click on `Create` and then `Create Empty`. This will create an invisible object.

Open it up on the inspector and give it the name "Spawn Point". Also, position it in the level where you think the enemies should spawn from.

## STEP 3: New script

Create a new javascript called `SpawnEnemy`.

In it, we'll have 4 variables:

- Public variable called `enemy` that's of type `GameObject`
- Public variable called `spawnTime` that's of type `float` with an initial value of `3f`
- Public variable called `canvas` that's of type `Canvas`
- Public variable called `healthPrefab` that's of type `GameObject`

Let's add the following line to the `Start` function:

```
InvokeRepeating ("Spawn", spawnTime, spawnTime);
```

Create a new function called `Spawn` and give it the following lines:

```
enemy.SetActive(false);
var newEnemy = Instantiate (enemy, transform.position, transform.rotation);
newEnemy.GetComponent(EnemyHealth).canvas = canvas;
newEnemy.GetComponent(EnemyHealth).healthPrefab = healthPrefab;
enemy.SetActive(true);
newEnemy.SetActive(true);
```

### STEP 4: Attach and set up the script

Attach the script to .... uh. What?

You should know what to attach it to.

Once you do, set it up! Again, you should know what to do:

![](http://i.imgur.com/3qRXB0F.png)

### STEP 5: TRY IT OUT

Also, make new spawn points!

For different enemies!

With different spawn times!
