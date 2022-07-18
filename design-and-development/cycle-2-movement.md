# Cycle 2 - Movement

## Design

### Objectives

* [x] Make the character automatically move along the screen
* [x] Allow the player to make the character jump by using the space bar
* [x] Make the screen scroll along with the character

### Usability Features

Controls - will be extremely simple and will be using the space bar to make the character jump. This makes the controls very easy to understand so the player doesn't have to spend a long amount of time learning how they work.

### Pseudocode for movement

```
Speed = 400
On Game Update( () => { 
    Move Right(Speed)
}) 
WhenSpaceBarIsPressed(() => {
    if player is grounded{
        make the character jump
    }
})

```

## Development

Initially I was unsure how to call an event every game update so I tried to create a game loop that repeatedly ran a certain line of code. However this caused my game to crash so I then looked it up on kabooms website and found that there was a function that did the same thing called onUpdate. I tried this and it worked perfectly.

```
 onUpdate(() => {
    player.move(SPEED, 0)
  })
```

The next thing I needed to add was the side scrolling camera, so that the character doesn't go off the edge of the screen. I found a line of code online that did this exact thing so I added it into my game scene.

```
 player.onUpdate(() => {
    var currCam = camPos();
    if (currCam.x < player.pos.x) {
    camPos(player.pos.x, currCam.y);
    }
  })
```

The final thing to do in this stage was to add the ability to jump. This wasn't too difficult and only took me a few minutes to add.

```
onKeyPress("space", () => {
    if (player.grounded()) {
      player.jump()
    }
  })
```

### Challenges

The biggest challenge here was finding out how to run something on each update of the game. I didn't know that there was a function already created that did this for me, so I tried to write the code on my own and it just caused the game to crash. However after finding the onUpdate function everything else was fine.

## Testing

| Test | Instructions        | What I expect to happen                        | What actually happened                              | Pass/Fail |
| ---- | ------------------- | ---------------------------------------------- | --------------------------------------------------- | --------- |
| 1    | Run Code            | The character to move across the screen        | The screen froze and the website stopped responding | Fail      |
| 2    | Run Code            | The character to move across the screen        | as expected                                         | Pass      |
| 3    | Run Code            | The camera to move along the level             | as expected                                         | Pass      |
| 4    | Press the Space bar | The character to jump when it is on the floor  | as expected                                         | Pass      |

### Evidence of Testing

![](<../.gitbook/assets/image (10).png>)

As you can see the camera has scrolled along with the character and it is jumping over a gap in the level.
