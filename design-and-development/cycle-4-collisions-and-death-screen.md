# Cycle 4 - Collisions and Death Screen

## Design

### Objectives

* [x] Add collision detection so that when the character hits an obstacle,  or falls off the map a game over screen appears
* [x] Design a game over screen

### Usability Features

Obstacles - Will be clearly visible so that the player is able to avoid them

Text - The text that appears one an obstacle is hit will be clear and instruct the user on how to navigate to the menu

### Pseudocode for  Collisions

```
If sprite collides with an obstacle {
    Run death scene
}

If sprite y position > 700 {
    Run death scene
}
```

## Development

I began by creating a death scene which displays a game over message and gives the user instructions on how to proceed back to the main menu screen. After creating the new scene I added in a line of text and positioned it correctly. Since I only used one line of text I positioned it in the middle of the screen as that made it look more symmetrical. I tried to keep the design simple and effective, as I don't want to waste too much time making these menus.

```javascript
scene("death", () => {
  add([
    text( "Game over press enter to return to the main menu", { size: 35 }),
    pos(vec2(500, 350)),
    origin("center"),
    color(255, 255, 255),
  ]);

  onKeyRelease("enter", () => {
    go("start");
  })
})
```

Then I added in a function that detects if the enter key is pressed. If this condition is met the scene changes and the user returns to the start screen.&#x20;

After this I began programming the collision mechanics into the game. I started with the obstacles and created two functions that detected whether or not the sprite had collided with an obstacle. I was initially unsure of how to do this but after searching online I found out that kaboom has a function already created that detects collisions for you. This made it far easier to program and only required 6 lines of code.

```javascript
player.onCollide("Spike V", () => {
    go("death")
  })
  player.onCollide("Spike H", () => {
    go("death")
  })
```

The second type of collision I needed to implement was one that detected if the sprite had fallen off the map. I initially just made an if statement that checked whether or not the the sprite position was below 700 which is the co-ordinate at the bottom of the screen.

```javascript
 if(player.pos.y > 700){
    go("death")
```

However this didn't work and I realised I had forgotten to add an update loop. After adding this in I ran it again and it worked straightaway.

```javascript
onUpdate(() =>{
  if(player.pos.y > 700){
    go("death")
    }
  })
```

### Challenges

I faced some small challenges while creating these collisions. Initially I was unsure how to create a collision function on my own and after about 10 minutes of searching I found out that there was a collision function already built into the kaboom library. The other challenge I faced was realising that I needed to add in an Update loop to my second function.&#x20;

## Testing

| Test | Instructions                              | What I expect to happen    | What actually happened                                          | Pass/Fail |
| ---- | ----------------------------------------- | -------------------------- | --------------------------------------------------------------- | --------- |
| 1    | Sprite collides with an obstacle          | Game over screen to appear | As expected                                                     | Pass      |
| 2    | Press enter while on the game over screen | The start screen to appear | As expected                                                     | Pass      |
| 3    | Sprite falls off the map                  | Game over screen to appear | The camera continued to scroll while the sprite was off the map | Fail      |

### Evidence of testing

#### Test 1

<figure><img src="../.gitbook/assets/Screenshot 2022-08-28 at 17.01.31.png" alt=""><figcaption></figcaption></figure>

After running the game and clicking start the square collided with the first spike. The game ended and this screen appeared.

#### Test 2

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

After the game ended and I was on the game over screen I pressed the enter key and the start screen appeared again.

#### Test 3

In order to test this I had to make a modification to the level. I made the gaps in between the level larger, allowing the square to fall through the gap and off the map.

```
[ 
  "                                                                             ",
  "                                                                             ",
  "                                                                             ",
  "                                                                            ",
  "                                                                             ",
  "                                                               <=============",
  "            +                         +              <==========            ",
  "=========================    ===    =====    =========                       "
  ],

]
```

After falling through this gap the game didn't end, and instead the screen just kept scrolling along as normal.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Here you can see that the screen continued to scroll along, but the square has fallen off the map.

## Changes due to faults found

After finding this fault in my game I checked through the code that was supposed to detect whether the player had fallen off the map. After reading the code I had written I realised that I had forgotten to add an update loop, which meant that the if statement wasn't constantly being checked. Below is the new code with the update loop added.

```javascript
onUpdate(() =>{
  if(player.pos.y > 700){
    go("death")
    }
  })
```

### Testing

| Test | Description                  | What I expect to happen        | What actually happened | Pass/Fail |
| ---- | ---------------------------- | ------------------------------ | ---------------------- | --------- |
| 4    | The player falls off the map | The game over screen to appear | As expected            | Pass      |

### Evidence of testing

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

After falling off the map the game ended and the death screen appeared. This test was passed.
