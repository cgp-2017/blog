---
title: "Show Enemy Health"
date: 2017-02-12 10:00
grade: secondary
published: true
---

# Show Enemy Health

We'll be showing health bars above enemies.

## STEP 1: Health bar Game Object

1. Add a `UI > Panel` to the Hierarchy. This will create a Canvas as well. Make
   sure in the inspector `Render Mode` is set to `Screen space — Overlay`.
2. Select the Panel, and rename it at the top of the Inspector to "HealthBar"
3. Inside the inspector, untick the `Image (script)` to disable the overlay background.
4. Add a Slider to the Canvas and __drag it inside the `HealthBar`__.
5. Click on the Slider. In the inspector:
    - Untick "Interactable"
    - Set "Transition" to `None`
6. Expand the Slider triangle. You should see a `Background`, a `Fill Area` and
   a `Handle Slide Area`.
7. Click on the `Handle Slide Area` and disable it by unticking the checkbox at
   the top of the inspector.
8. Click on `Background`. Disable its `Image (Script)` like you did with the HealthBar.
9. Expand the `Fill Area` and select `Fill`. Here, set the scale to:
    - X: 1
    - Y: 3
    - Z: 1
10. With `Fill` still selected, in the `Image Script` area, you should choose
    the color for your health bar. (I chose green)

In the end, it should look like this:

![](http://i.imgur.com/4paWQwi.png)

## STEP 2: A new prefab

1. Drag the `HealthBar` into your `prefabs` folder.
2. Delete the `HealthBar` from the Hiearchy (WARNING: Only do this after creating the prefab)

## STEP 3: Hook up health bar to enemies

Let's modify our enemy health script (__You should know which one it is__).

1. Add the following __public__ variables to your enemy health script:
    - `canvas`: The type is `Canvas`
    - `healthPrefab`: The type is `GameObject`
    - `healthPanelYPosition`: The type is `float` and the value is `2.5f`
2. Add the following __private__ variables to your enemy health script:
    - `healthPanel`: The type is `GameObject`
    - `healthSlider`: The type is `UnityEngine.UI.Slider`
    - `maxHealth`: The type is `int`
3. In the Start function, make the `maxHealth` value equals to that of `enemyHealth`.
4. In the Start function, make the `healthPanel` value equals to that of `Instantiate(healthPrefab)` (that is, make a new object of healthPrefab).
5. Add this line to the Start function: `healthPanel.transform.SetParent(canvas.transform, false);`
6. In the Start function, make the `healthSlider` value equals to `healthPanel.GetComponentInChildren(UnityEngine.UI.Slider)`

## STEP 4: Display the health bar

1. In the Update method of the health script, after the if statement add this line: `healthSlider.value = parseFloat(enemyHealth)/parseFloat(maxHealth);`
2. Add the following three lines below that:

```javascript
var worldPos : Vector3 = Vector3(transform.position.x, transform.position.y + healthPanelYPosition, transform.position.z);
var screenPos : Vector3 = Camera.main.WorldToScreenPoint(worldPos);
healthPanel.transform.position = Vector3(screenPos.x, screenPos.y, screenPos.z);
```

## STEP 5: Set the public variables

Inspect one of your enemies with the EnemyHealth script.

You'll see two variables that need to be set:

![](http://i.imgur.com/b1BP8lM.png)

Think you can figure out what their values should be? You can easily figure it
out from clicking on the little circle next to the field.

## STEP 6: You're done! Try it out.

