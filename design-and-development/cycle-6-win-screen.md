# Cycle 6 - Win Screen

## Design

### Objectives

* [x] Create a portal at the end of the game that if hit sends you to a win screen

### Usability Features

* [x] The win screen should give clear instructions as to how to navigate back to the main menu

### Pseudocode

```
if character touches portal{
    go death scene
}

```

## Development

Creating a win screen wasn't too difficult and followed a similar method to making the death screen. Firstly I downloaded a portal image that I would use for my finish line.&#x20;

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>Portal Sprite</p></figcaption></figure>

I then added the load code for this sprite and gave it the name "Portal".

```javascript
loadSprite("Portal", "sprites/Portal.png");
```

I had previously added the character "0" at the end of the level which is the character I will be mapping to the portal sprite.

To do this I needed to add the portal into the level configuration, giving it all the functions it needs as well as its own unique "Win" tag. This tag would allow me to reference it later on.

```javascript
"0": () => [
    sprite("Portal"),
    area(),
    solid(),
    scale(0.5,0.5),
    origin("bot"),
    "Win"
  ]
```

I then began writing the code that would sense when the character comes into contact with the portal. This was very similar to the spike collision code but instead changes to the win scene rather than the death scene.

```javascript
player.onCollide("Win", () =>{
    go("win")
  })
```

