---
title: "Enemy Damage Sound"
date: 2017-02-05 11:00
grade: secondary
published: true
---

# Add an Enemy Damage Sound

The assets we downloaded actually include hurt sounds for the Hellephant, the Zombear and the Zombunny.

Go to `Assets > Audio > Effects` to check them out!

![](http://i.imgur.com/BBfR46v.png)

## 1. Add `AudioSource` component

- choose an enemy in the `hierarchy`
- scroll to the bottom in its `inspector`
- click on "Add Component"
- select `AudioSource`
- drag the right sound for your enemy from `Assets > Audio > Effects` onto the `AudioClip` field
- untick "Play On Awake"

![](http://i.imgur.com/W1TlX9Y.png)

## 2. Add Variable in `EnemyHealth` script

```javascript
public var hurtAudio : AudioSource;
```

Add to `start` function:

```javascript
hurtAudio = GetComponent(AudioSource);
```

## 3. Play the sound

- Open the `Shooting` script
- Add in the `Shoot` function below the line reducing the enemyHealth:

```javascript
enemyhealth.hurtAudio.Play();
```

## 4. Test your game

## 5. Add to the other enemy types
- all enemy types use the same scripts, you don't need to change them further
- add the `AudioSource` component
- choose the right sound effect
- only do this once per enemy type! Make a prefab, don't do it for every single Hellephant!


