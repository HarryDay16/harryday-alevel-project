# Cycle 5 - Enemies

## Design

### Objectives

* [x] Create enemies that appear throughout the level
* [x] Make the enemies move across the screen towards the player
* [x] End the game if the player makes contact with an enemy

### Usability Features

Visibility - The enemies will be clearly visible so that the player will know to avoid them

### Pseudocode for New Level design

```
levels = [
[ 
  "                                                                             ",
  "                                                                             ",
  "                                                                             ",
  "                                                                            ",
  "                                                                             ",
  "                                                               <=============",
  "                        x                        x   <==========            ",
  "======================================================                       "
  ],
  ]
```

### Pseudocode for sprite configuration

```
load in Enemy Sprite as "Enemy" 

 "x" set to sprite("Enemy"){
        area(),
        gravity(),
        origin("bottom")
    }
```

### Pseudocode for movement and collisions&#x20;

```
SPEED = 280

OnUpdate{
    if enemy is on the screen {
        Move enemy left at SPEED
    }
}

if player touches an enemy{
    go to death scene
}
```

## Development

I began by finding a suitable sprite for my enemies. I looked online and downloaded a sprite pack, and selected the below sprite. This was because it has a relatively simple shape, and I think it will fit the games aesthetic nicely.

<figure><img src="../.gitbook/assets/image (12) (1).png" alt=""><figcaption><p>An image of the enemy sprite</p></figcaption></figure>

After considering how I could introduce enemies into the game I thought that the best way to do it would be to make the enemies move across the screen in the opposite direction of the sprite being controlled by the user. This seemed pretty manageable and would introduce a new element into the game.

The first thing I did was load the sprite in by adding a line of code at the top of the page.

```javascript
loadPedit("Enemy", "sprites/Enemy.pedit");
```

After this I modified the level. I removed the spikes and the gaps. This will allow me to test it more easily. I then added in two "x" characters, which will be mapped to the enemy sprite in the level config.

```javascript
[ 
  "                                                                             ",
  "                                                                             ",
  "                                                                             ",
  "                                                                            ",
  "                                                                             ",
  "                                                               <=============",
  "                        x                        x   <==========            ",
  "======================================================                       "
  ],
```

I then went into the level config and assigned the character "x" to the sprite as well as adding the necessary functions and giving it a "Move" tag and an "Enemy" tag. These tags would later allow me to reference the enemy sprites more easily. I also resized the sprite until it appeared on the screen at a size that I considered to be appropriate.

```javascript
  "x": () => [
    sprite("Enemy"),
    area(),
    body(),
    origin("bot"),
    scale(3,3),
    "Enemy",
    "Move"
  ],
```

Then I went down to the main game scene and began writing the code that would make the enemies move and result in the game ending on a collision.

Since I had already programmed the collisions for the spikes this was a very simple ask and all I needed to do was copy and paste the same code but change the tag that I was referencing.&#x20;

```javascript
player.onCollide("Enemy", () => {
    go("death")
  })
```

The enemy movement was more difficult to program and it took me multiple attempts until I got it to work how I wanted it to. Initially I used the onUpdate function and tried referencing the enemy later, however this wasn't working well and I couldn't figure out how to make it work. After researching the problem I found the action function which makes each sprite with the referenced tag perform an action on every update - this solved my problem.&#x20;

I then needed to make the sprite move left but only when it was on the screen. My first thought was to include an if statement to check if the enemy's x co-ordinate was > 1000 which is the width of the screen. The code looked like this:

```javascript
action("Move",(e) => {
  if(e.pos.x < 1000){
    e.move(-SPEED, 0) 
  }
})
```

### Challenges

Programming the movement for the enemies was the biggest challenge as I was intially unsure how to create a loop allowing me to move the enemy constantly. However, after finding the action() function in the kaboom docs the problem became much easier.

## Testing

| Test | Instructions                                      | What I expect to happen                      | What actually happened                                                                                                                                 | Pass/Fail |
| ---- | ------------------------------------------------- | -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- |
| 1    | An enemy appears on the screen                    | The enemy to start moving across the screen  | The enemies that appeared on the  initial camera view moved as expected, but the enemies that appeared after the camera had scrolled along didn't move | Fail      |
| 2    | The enemy makes contact with the player character | The death screen appears                     | As expected                                                                                                                                            | Pass      |

### Evidence of testing

#### Test 1

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>The first enemy</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>The second enemy</p></figcaption></figure>

I conducted this test and the sprite that was initially on the screen moved across as expected, however the other sprite didn't move at all and stayed stationary.

#### Test 2

<figure><img src="../.gitbook/assets/image (3) (4).png" alt=""><figcaption></figcaption></figure>

This test was successful and after making contact with either one of the enemies this screen appeared.

## Changes due to faults found

After failing the first test I looked back through the code controlling enemy movement.

```javascript
action("Move",(e) => {
  if(e.pos.x < 1000){
    e.move(-SPEED, 0) 
  }
})
```

I shortly realised what the problem was and why only the first sprite was moving. The co-ordinates on the screen change as the camera scrolls along, so the sprites that had been placed further along would never reach below an x co-ordinate of 1000. My solution for this was to track the camera position and add on a value so that the enemies would begin moving when they appeared on the screen. Since the camera position was in the middle of the screen I just had to add on 500 so that the enemies would move when they reach the edge of the screen. The code looked like this:

```javascript
 action("Move",(e) => {
    if(e.pos.x < 500 + camPos().x){
      e.move(-SPEED, 0)    
    }        
  })
```

After reviewing this section I also realised that the code I had written was inefficient as the enemies are still moving even when they are off the screen. This would waste processing power and could make the game run more slowly as I expand the level.

In order to fix this I created another if statement in the action function so that when the enemies reach the opposite end of the screen they are removed from the scene. This was very simple to add and the final function looked like this:

```javascript
action("Move",(e) => {
    if(e.pos.x < 500 + camPos().x){
      e.move(-SPEED, 0)    
    }
    if(e.pos.x < camPos().x - 500){
      e.destroy()
    }           
  })
```

This should make my game run more smoothly in the future and prevent it from becoming too buggy.

## Testing

| Test            | Description                  | What I expect to happen                 | What actually happened | Pass/Fail |
| --------------- | ---------------------------- | --------------------------------------- | ---------------------- | --------- |
| <p></p><p>3</p> | The enemies appear on screen | Them to move along at a fixed velocity. | As expected            | Pass      |

### Proof of testing

#### Test 3

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption><p>The first enemy</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1) (4).png" alt=""><figcaption><p>The second enemy</p></figcaption></figure>

This time both enemies moved as expected, travelling horizontally towards the player. You can see that the second enemy has moved away from the horizontal spike and will make contact with the player earlier.
