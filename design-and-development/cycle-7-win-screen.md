# Cycle 7 - Win Screen

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

I then began writing the code that would detect when the character comes into contact with the portal. This was very similar to the spike collision code but instead changes to the win scene rather than the death scene.

```javascript
player.onCollide("Win", () =>{
    go("win")
  })
```

After this I started designing the win scene. I started by creating a new scene called "win" and added in some text saying that the player had won. I also gave clear instructions as to how to return to the main menu. I added in some other tags which would position the text correctly and make it the right color.&#x20;

```javascript
scene("win", () => {
  add([
    text("You win! Press enter to return to the main menu", { size: 24 }),
    pos(vec2(500, 350)),
    origin("center"),
    color(255, 255, 255),
  ]);

  onKeyRelease("enter", () => {
    go("start");
  })
});
```

I then needed to create a function to detect if the enter key was pressed. This can easily be done in kaboom as there is already a function made to detect key presses, so all I had to do was call the function and run the start screen if the enter key was pressed.

<figure><img src="../.gitbook/assets/image (3) (4).png" alt=""><figcaption><p>Screenshot of the win screen</p></figcaption></figure>

### Challenges

The biggest challenge I faced in this section was getting the menu to look good, and sizing the text correctly. It took me a few attempts until I sized it correctly, and the only way to approach it was through trial and error. I had the same issue when sizing the portal, and the first time I tried putting it into the game it was far too big, causing a collision to occur far too early.&#x20;

## Testing

| Test | Instructions                 | What I expect to happen                                             | What actually happened | Pass/fail |
| ---- | ---------------------------- | ------------------------------------------------------------------- | ---------------------- | --------- |
| 1    | Run the level                | The portal to appear at an appropriate size at the end of the level | As expected            | Pass      |
| 2    | Make contact with the portal | The win screen to appear                                            | As expected            | Pass      |

### Evidence of testing

