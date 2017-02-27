---
title: "Make dead enemies disappear"
date: 2017-02-15 12:00
grade: secondary
published: true
---

#Make dead enemies disappear

- Before, we just used `Destroy(this.gameObject);` to kill the enemy
- we stopped using this command to instead use the `dying animation`
- how can we do both?

You can use the `Destroy()` command in more than one way!
- `Destroy(Hellephant);`
  - This just destroys the Hellephant - no time to see the animation!
- `Destroy(Hellephant, 2);`
  - This also destroys the Hellephant **BUT** only after 2 seconds - just enough time to see the animation.
  
So where do we put it in our code?
- Open the `EnemyHealth` script
- In the update function, there is an `if statement` checking if the enemy's health is lower than 0
  - Inside are the two lines:
    - `var animationTrigger : String = "Dead";`
    - `this.GetComponent(Animator).SetTrigger(animationTrigger);`
  - Add the `Destory()` function underneath:
    - `Destroy(gameObject, 2);`
    
That's it!

Test your game.

If you're done, move on to the next blog post. It's going to make hitting enemies feel more satisfying.

