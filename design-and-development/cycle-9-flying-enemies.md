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



<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Initially I found this function online which makes enemies move back and forward at a set distance

```javascript
function patrol(distance = 100, speed = 50, dir = 1) {
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
}ja
```

I pasted this code into my javascript file and the added the patrol component to&#x20;
