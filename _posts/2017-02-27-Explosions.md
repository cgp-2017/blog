---
title: "Explosions"
date: 2017-02-27 12:00
grade: secondary
published: true
---
## Intro to Particle Systems
### or
# Let's Add Some Explosions!!!


First we need to add some new assets:
- Go to `Assets > Import Package`
- Choose `Particle Systems`
- A small window will open, click `[Import]`

![](http://i.imgur.com/4gjWPO9.png)

## Adding Explosions to Our Game

- We want to change our `Shoot.js` script, so that an explosion appears everytime you hit something!
- So let's open the `Shoot.js` script

Remember that we added the Enemy Health bars with the `Instantiate()` function? We'll use it now to make an explosion appear.

- Add a varible at the top of the script:
  - it's **public**
  - the name should be `explosionPrefab`
  - the type should be `GameObject`
- Inside the `Shoot()` function, inside the `if statement`, add this line:
  - Instantiate (explosionPrefab, shootHit.point, Quaternion.identity);
- Save the script and return to Unity
- If you entered the code correctly, a new text field called `Explosion Prefab` appeared in the `Shoot` component of `FPS Controller > GunBarrelEnd`
  - In the `Assets` folder navigate to `Assets > Standard Assets > ParticleSystems > Prefabs`
  - Drag the `Explosion` prefab onto the `Explosion Prefab` text field.
  
![](http://i.imgur.com/jnkoD6m.png)
  
  
  You're done! Test the game!
