# Cycle 9 - Flying Enemies

## Design

### Objectives

* [x] Create a new enemy sprite
* [x] Make the enemy fly above the player on a set patrol, moving back and forward
* [x] Allow the player to click on the enemies and make them disappear
* [x] Add one to the bonus score for each enemy killed
* [x] Display the score at the end of the game

### Key Variables and Functions

| Variable/Function name | Use                                                                                         |
| ---------------------- | ------------------------------------------------------------------------------------------- |
| patrol()               | A function that I will create, making the enemies move back and forward at a fixed distance |
| startingPos            | Contains the starting co-ordinates of the enemy.                                            |
| distance               | A set distance that the enemy will travel along its patrol                                  |
| dir                    | Set to +1 or -1 and represents the direction                                                |
| speed                  | Set to a constant value that controls the speed of the enemies                              |
| move()                 | Moves the enemy at a set velocity and angle                                                 |

## Pseudocode for moving enemies

```
function patrol(distance = 30, speed = 280, dir = 1){
        if pos.x < startingPosition.x - distance{
              dir = -1  
        }
        if pos.x > startingPosition + distance{
              dir = 1
        }
        move(dir*speed,0)
    }
```

## Pseudocode for clicking on enemy

```
// Some code
```

## Development

### Initial set up

I started by designing a new sprite and loaded it in.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>Flying enemy sprite</p></figcaption></figure>

Here I added a new line below the rest of the loaded assets, which loads in the flying enemy sprite.

```javascript
// load assets
loadPedit("Floor", "sprites/Floor.pedit");
loadPedit("Spike V", "sprites/Spike V.pedit");
loadPedit("Character", "sprites/Character.pedit");
loadPedit("Spike H", "sprites/Spike H.pedit");
loadSprite("Slime", "sprites/Slime.png");
loadSprite("Portal", "sprites/Portal.png");
loadPedit("Flying Enemy", "sprites/Flying Enemy.pedit");
```

I then added a new line in the level configuration, mapping the sprite to the character "£", and giving it the necessary functions. I also added the patrol function, which I will be creating later.

```javascript
 // Flying Enemy configuration
  "£": () => [
    sprite("Flying Enemy"),
    area(),
    origin("bot"),
    scale(2,2),
    patrol()
  ],
```

Then I modified the first section of the level and added in a flying enemy. This section is very simple, and will allow me to test the enemy easily.

```javascript
 // Section one of Level
  [
  "                                                                      ",
  "              £                                                       ",
  "                                                                      ",
  "                                                                      ",
  "                                                                      ",
  "                                 +                              <=====",
  "              +++      ++       <=      +++           <===========    ",
  "==================================================    <=              "
  ]
```

### Designing the patrol function

Initially I found this function online which makes enemies move back and forward at a set distance. I pasted this code into my JavaScript file and made a few small modifications

```javascript
function patrol(distance = 30, speed = 280, dir = 1) {
  return {
    id: "patrol",
    require: ["pos", "area",],
    startingPos: vec2(0, 0),
    add() {
      this.startingPos = this.pos;
      this.on("collide", (obj, side) => {
        if (side === "left" || side === "right") {
          dir = -dir;
        }
      });
    },
    update() {
      if (Math.abs(this.pos.x - this.startingPos.x) >= distance) {
        dir = -dir;
      }
      this.move(speed * dir, 0);
    },
  };
}
```

It works by defining the objects initial position and then moving it at a constant speed. The direction then changes depending on where the object is relative to the starting position.

### Testing the initial patrol function

| Test | Instructions           | What I expect to happen                                    | What actually happened                                                   | Pass/Fail |
| ---- | ---------------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------ | --------- |
| 1    | Run the modified level | The Enemy should move back ad forward at a constant speed  | The enemy moved forward at a constant speed but never changed direction. | Fail      |

### Proof of testing

#### Test 1

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Here the enemy is moving to the right at a fixed speed. It is travelling more slowly than the player character.&#x20;

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

A few seconds later the enemy is still moving in the same direction and has not moved to the opposite direction. After modifying the distance to equal 1, I ran the code again and I got the same result.&#x20;

### Re-designing the patrol function

After this I designed a completely new patrol function. My new design was more simple and logical, and I found it easier to understand since I had created it from scratch.

<pre class="language-javascript"><code class="lang-javascript"><strong>// function for enemy movement
</strong>// defining distance, speed and direction constants) 
<strong>function patrol(dis = 100,speed = 280,dir = -1){
</strong>  return {
    // setting the function id to "patrol"
    id: "patrol",
    // these attributes are required for the function to work
    require: ["pos", "area",],
    // contains setup code
    add() {
      // defines the starting position
      this.startingPos = this.pos.x 
      // defines the ending position
      this.endingPos = this.startingPos + dis
    },
    // runs on every update of the game
    update() {
      // move at a velocity of speed*dir, at an angle of 0
      this.move(speed*dir,0)
      // when the object's x co-ordinate is greater than the ending position run the contents
      if(this.pos.x > this.endingPos){
        // Set the direction to be negative
        dir = -1
      }
      // when the object's x co-ordinate is less than the starting position minus the distance, run the contents
      if(this.pos.x &#x3C; this.startingPos - dis){
        // make the direction positive
        dir = 1
      }  
    }
  }
}
</code></pre>

After this I modified the finished level and added in some of these enemies along the level.

```javascript
[ 
// completed level
"                      £                                 £                                   £                             +++                  x         x              x  ++                      +                                           +                    £                                  ",
  "                                                                                                                    <========================================================                  x  <=                     x             x      <=         +                                             ",
  "                                                                                                                    <=                                                      ===========================   ======================================         =                 +            0              ",
  "                                                                                                            <=========                                                                                                                         ===========         +++    <=                           ",
  "                                                                       ++     +       +        +      <=======                                                                                                                                           =================================             ",
  "                                 +                              <==================+++=       <=========                                                                                                             £                                                                                 ",
  "              +++      ++       <=      +++           <===========                ==============                                             £                                                                                                            £                                            ",
  "==================================================    <=																													          "                                                                                                                                                                                                                                               
  ]
```

### Testing re-designed function

| Test | Instructions           | What I expect to happen                                       | What actually happened | Pass/Fail |
| ---- | ---------------------- | ------------------------------------------------------------- | ---------------------- | --------- |
| 2    | Run the modified level | The flying enemy to move back and forward at a constant speed | As expected            | Pass      |

### Proof of testing

#### Test 2

{% file src="../.gitbook/assets/Flying enemy test.mov" %}

In the clip above it shows the enemy moving back and forward on a set patrol path. Therefore this test was passed

## Making them clickable and calculating bonus score

Here I added a "clickable" tag in the configuration, allowing me to reference the flying enemies specifically.

```javascript
// Flying Enemy configuration
  "£": () => [
    sprite("Flying Enemy"),
    area(),
    origin("bot"),
    scale(2,2),
    patrol(),
    "clickable"
  ],
```

Then I added some code in the main game scene, which made the enemies disappear when they were clicked on.

```javascript
// click detection on flying enemies
  onClick("clickable", (e) => {
    // destroy the enemy
    destroy(e)
   })
```

I then needed to design a point counter, which will show how many enemies have been killed. I started by adding a killCount variable, and then a line of code into the onClick() function in order to track how many enemies have been killed.

```javascript
// setting kill count variable to zero
let killCount = 0
// click detection on flying enemies
  onClick("clickable", (e) => {
    // destroy the enemy
    destroy(e)
    // add 1 to the kill count
    killCount += 1
})
```

Then I passed the killCount variable back through all of the go("death") and go("win") functions so that it could be displayed at the end of the game. After this I edited the death and win scenes, adding in the below code, which displays the killCount at the end of the game.

```javascript
add([
    text("enemies killed: "+killCount,{size:30}),
    pos(vec2(500,450)),
    origin("center"),
    ])
```

### Final test

| Test | Instruction       | What I expect to happen    | What actually happened | Pass/Fail |
| ---- | ----------------- | -------------------------- | ---------------------- | --------- |
| 3    | Click on an enemy | The enemy should disappear | As expected            | Pass      |

### Proof of testing

#### Test 3

{% file src="../.gitbook/assets/Enemy click test.mov" %}

In the clip above you can see that the enemy disappears when I click on it, and then after I hit a spike the kill count is shown below the prompt on the death screen. Therefore this test was passed

## Challenges

Throughout this development cycle I faced many challenges. When designing the patrol function I was initially unsure as to how these custom components needed to be set up. After researching I was able to figure this out and understand what each section of the function did, and where each piece of code needed to be.&#x20;
