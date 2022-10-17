# Cycle 3 - Movement and side scrolling camera

## Design

### Objectives

* [x] Make the character automatically move along the screen
* [x] Allow the player to make the character jump by using the space bar
* [x] Make the screen scroll along with the character

### Usability Features

Controls - will be extremely simple and will be using the space bar to make the character jump. This makes the controls very easy to understand so the player doesn't have to spend a long amount of time learning how they work.

### Pseudocode for movement

```
Speed = 100
On Game Update( () => { 
    Move Right(Speed)
}) 
WhenSpaceBarIsPressed(() => {
    if player is grounded{
        make the character jump
    }
})

if player.x.pos > camera.x.pos{
    cameraPos(player.x.pos, camera.y.pos) 
}
```

## Development

I began this cycle by defining a new constant at the start of the game scene. This is called SPEED and will remain the same throughout the game. I set it to 100 for now, but I can easily change it later on.

```javascript
const SPEED = 100;
```

Initially I was unsure how to call an event every game update so I tried to create a game loop that repeatedly ran a certain line of code, however when I ran the code it caused my game to crash. This was likely due to the while loop being called too quickly.

```javascript
let loop = true
while(loop){
  player.move(SPEED,0)
}
```

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption><p>This is the error message that appeared</p></figcaption></figure>

After researching the problem and looking through kabooms website I found that there was a function that was able to run on every game update. This should work better as the speed of the loop matches the speed of the game.

```javascript
 onUpdate(() => {
    player.move(SPEED, 0)
  })
```

<figure><img src="../.gitbook/assets/image (2) (4).png" alt=""><figcaption></figcaption></figure>

The image above shows that the character has moved across the screen. It went through the spike due to it not being solid, and also made it over the gap in the level due to the character being much larger than the gap. In the future I will need to make adjustments to the level and make the gaps wider. As well as this the square moved quite slowly. After some trial and error I decided that the speed should be set to 280 as I felt it fitted the dimensions of the level the best.

```javascript
const SPEED = 280;
```

The next thing I needed to add was the side scrolling camera, so that the player doesn't go off the edge of the screen. After researching the problem I found a chunk of code online that did this exact thing so I added it into my game scene.

```javascript
 player.onUpdate(() => {
    var currCam = camPos();
    if (currCam.x < player.pos.x) {
    camPos(player.pos.x, currCam.y);
    }
  })
```

This works by constantly checking the camera position and moving it to the position of the player.

The final thing to do in this stage was to add the ability to jump. This wasn't too difficult and only took me a few minutes to add. Kaboom has a built in function that checks if a key is pressed, and can also check to see if a sprite is grounded. I used both of these features in the chunk of code below that allows the player to jump only when it is on the ground.

```javascript
onKeyPress("space", () => {
    if (player.grounded()) {
      player.jump()
    }
  })
```

### Challenges

The biggest challenge here was finding out how to run something on each update of the game. I didn't know that there was a function already created that did this for me, so I tried to write the code on my own and it just caused the game to crash. However after finding the onUpdate function everything else was fine.

## Testing

| Test | Instructions        | What I expect to happen                        | What actually happened | Pass/Fail |
| ---- | ------------------- | ---------------------------------------------- | ---------------------- | --------- |
| 1    | Run Code            | The square to move and the camera to follow    | as expected            | Pass      |
| 2    | Press the Space bar | The character to jump when it is on the floor  | as expected            | Pass      |

### Evidence of Testing

#### Test 1

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Here you can see that the square has moved across the level and the camera has followed it.  It currently passes through the spikes and over the gaps. I will change this in later cycles.

#### Test 2

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

Test 2 was a success, and you can see the square jumping while it moves through the level. I also tried pressing the space bar while it was in the air and it did not jump a second time.
