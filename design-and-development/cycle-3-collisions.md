# Cycle 3 - Collisions

## Design

### Objectives

* [x] Add collision detection so that when the character hits an obstacle,  or falls off the map a game over screen appears

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

I began by creating a death scene which said game over and displayed instructions on how to proceed back to the menu screen. I made it very simple for now, however once everything else is completed I intend to go back and improve these menu screens.&#x20;

After this I began programming the collision mechanics into the game. I started with the obstacles and created two functions that detected whether or not the sprite had collided with an obstacle. I was initially unsure of how to do this but after searching online I found out that kaboom has a function already created that detects collisions for you. This made it far easier to program and only required 6 lines of code.

```
player.onCollide("Spike V", () => {
    go("death")
  })
  player.onCollide("Spike H", () => {
    go("death")
  })
```

The second type of collision i needed to implement was one that detected if the sprite had fallen off the map. I initially just made an if statement that checked whether or not the the sprite position was below 700 which is the co-ordinate at the bottom of the screen. However this didn't work and I realised I had forgotten to add an update loop. After adding this in I ran it again and it worked straightaway.

```
onUpdate(() =>{
  if(player.pos.y > 700){
    go("death")
    }
  })
```

### Challenges

I faced some small challenges while creating these collisions. Initially I was unsure how to create a collision function on my own and after about 10 minutes of searching I found out that there was a collision function already built into the kaboom library. The other challenge I faced was realising that I needed to add in an Update loop to my second function.&#x20;

## Testing

| Test | Instructions                     | What I expect to happen    | What actually happened                                          | Pass/Fail |
| ---- | -------------------------------- | -------------------------- | --------------------------------------------------------------- | --------- |
| 1    | Sprite collides with an obstacle | Game over screen to appear | The Game over screen appeared                                   | Pass      |
| 2    | Sprite falls off the map         | Game over screen to appear | The camera continued to scroll while the sprite was off the map | Fail      |
| 3    | Sprite falls off the map         | Game over Screen to appear | The game over screen appeared                                   | Pass      |

### Evidence of testing

<figure><img src="../.gitbook/assets/Screenshot 2022-08-28 at 17.01.31.png" alt=""><figcaption><p>This is the game over screen that appeared after the sprite fell off the map or struck an obstacle</p></figcaption></figure>
