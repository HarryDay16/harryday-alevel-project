# Cycle 9 - Flying Enemies

## Design

### Objectives

* [x] Create a new enemy sprite
* [x] Make the enemy fly above the player on a set patrol, moving back and forward
* [x] Design a health bar for the player
* [x] Make the enemy shoot at the player and deal damage

### Key Variables and Functions

| Variable/Function name | Use                                                                                         |
| ---------------------- | ------------------------------------------------------------------------------------------- |
| patrol()               | A function that I will create, making the enemies move back and forward at a fixed distance |
| startingPos            | Contains the starting co-ordinates of the enemy.                                            |
| distance               | A set distance that the enemy will travel along its patrol                                  |

## Pseudocode for moving enemies

```
function patrol(){
    

    }
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

