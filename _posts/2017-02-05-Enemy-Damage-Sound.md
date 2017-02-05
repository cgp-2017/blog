---
title: "Enemy Damage Sound"
date: 2017-01-15 10:00
grade: secondary
---

# Add an Enemy Damage Sound

The assets we downloaded actually include death and hurt sounds for the Hellephant, the Zombear and the Zombunny.

Go to `Assets > Audio > Effects` to check them out!

[screen shot]

## 1. Add `AudioSource` component

- choose an enemy in the `hierarchy`
- scroll to the bottom in its `inspector`
- click on "Add Component"
- select `AudioSource`

[ screen shot]

## 2. Add Variable in `EnemyHealth` script

```javascript
private var hurtAudio : AudioSource;
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


## 4. Choose which sound to play
- in enemy's `Inspector`, in the `EnemyHealth` script componenent, you now have the `hurtSound` field
- drag the right sound for your enemy from `Assets > Audio > Effects` onto that field


## 5. Test your game

## 6. Add to the other enemy types
- all enemy types use the same scripts, you don't need to change them further
- add the `AudioSource` component
- choose the right sound effect
- only do this once per enemy type! Make a prefab, don't do it for every single Hellephant!


# Add an Enemy Death Sound

You follow the same steps as above except:

- replace 'hurt' with 'death' when adding variables
- for **3. Play the sound**:
  - add the line ** in the `EnemyHealth` script**
  - inside the if statement
  

