# Cycle 7 - Win Screen

## Design

### Objectives

* [x] Create a portal at the end of the game that if hit sends you to a win screen

### Usability Features

* [x] The win screen should give clear instructions as to how to navigate back to the main menu

### Pseudocode for Sprite configuration

```
load in Portal Sprite as "Portal" 

 "0" set to sprite("Portal"){
        area(),
        solid(),
        origin("bottom"),
        "Win"
    }

```

### Pseudocode for Collision

```
If player collides with "Win" {
        go to win screen
    }
```

### Pseudocode for Win Screen

```
If enter key is pressed {
        go to home screen
    }
```

## Development

Creating a win screen wasn't too difficult and followed a similar method to making the death screen. Firstly I downloaded a portal image that I would use for my finish line.&#x20;

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption><p>Portal Sprite</p></figcaption></figure>

I then added the load code for this sprite and gave it the name "Portal".

```javascript
loadSprite("Portal", "sprites/Portal.png");
```

I had previously added the character "0" at the end of the level which is the character I will be mapping to the portal sprite.

To do this I needed to add the portal into the level configuration, giving it all the functions it needs as well as its own unique "Win" tag. This tag would allow me to reference it later on.

<pre class="language-javascript"><code class="lang-javascript"><strong>"0": () => [
</strong>    sprite("Portal"),
    area(),
    solid(),
    scale(0.5,0.5),
    origin("bot"),
    "Win"
  ]
</code></pre>

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

I also added a couple of lines to detect if the enter key was pressed. This can easily be done in kaboom as there is already a function made to detect key presses, so all I had to do was call the function and run the start screen if the enter key was pressed.

### Challenges

The biggest challenge I faced in this section was getting the menu to look good, and sizing the text correctly. It took me a few attempts until I sized it correctly, and the only way to approach it was through trial and error. I had the same issue when sizing the portal, and the first time I tried putting it into the game it was far too big, causing a collision to occur far too early.&#x20;

## Testing

| Test | Instructions                  | What I expect to happen                                             | What actually happened | Pass/fail |
| ---- | ----------------------------- | ------------------------------------------------------------------- | ---------------------- | --------- |
| 1    | Run the level                 | The portal to appear at an appropriate size at the end of the level | As expected            | Pass      |
| 2    | Make contact with the portal  | The win screen to appear                                            | As expected            | Pass      |
| 3    | Press enter at the win screen | To return to the main menu                                          | As expected            | Pass      |

### Evidence of testing

#### Test 1

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Here you can see that the portal did appear at the end of the level. Therefore this test was a success.

#### Test 2

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

After coming into contact with the portal I was instantly sent to the win screen which is shown above. This test was passed.

#### Test 3

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

I pressed enter on the win screen and was immediately sent back to the title screen. This test was passed.
