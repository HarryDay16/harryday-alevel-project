# Cycle 4 - Enemies Part 1

## Design

### Objectives

* [x] Create enemies that appear throughout the level
* [x] Make the enemies move across the screen towards the player
* [x] End the game if the player makes contact with an enemy

### Usability Features

Visibility - The enemies will be clearly visible so that the player will know to avoid them

### Pseudocode for Enemies

```
OnUpdate{
    if enemy is on the screen{
        Move enemy left
    }

}
```

## Development

I began by designing the enemy sprite for the game. I kept this design pretty simple, but so it was still clear that they were enemies that needed to be avoided.&#x20;

After considering how I could introduce enemies into the game I thought that the best way to do it would be to make the enemies move across the screen in the opposite direction of the sprite being controlled by the user. This seemed pretty manageable and would introduce a new element into the game.

