# 2.1 Design Frame

## Systems Diagram

![](<../.gitbook/assets/image (8) (1).png>)

This diagram shows the different parts of the game that I will focus on creating. I have split each section into smaller sub-sections. Throughout the development stage, I will pick one or two of these sections to focus on at a time to gradually build up and piece together the game. I have broken the project down this way as it roughly corresponds to the success criteria.

## Usability Features

Usability is an important aspect to my game as I want it to be accessible to all. There are 5 key points of usability to create the best user experience that I will be focusing on when developing my project. These are:

### Effective

Users can achieve the goal with completeness and accuracy. To do this, I will make it easy for the players to realise that they need to reach a goal in order to complete a level. I will make this goal clear to see so there is no confusion over where the players need to go.

#### Aims

* Create a clear goal to reach to determine the end of a level
* Create a clear goal for any multiplayer modes

### Efficiency

The speed and accuracy to which a user can complete the goal. To do this, I will create a menu system which is easy to navigate through in order for to find what you are looking for. The information which is more important can be found with less clicks.

#### Aims

* Create a menu system that is quick and easy to navigate through
* Create a controls system that isn't too complicated but allows the player to do multiple actions

### Engaging

The solution is engaging for the user to use. To do this, I will create 5 levels and an online multiplayer mode to keep the players engaged and allow them to have fun while playing the game. Using vector style art will also make the game nicer to look at than blocks, so will draw more people in, keeping them engaged.

#### Aims

* Create a series of levels to work through
* Create a multiplayer mode to play
* Incorporate a style of game art the suits the game

### Error Tolerant

The solution should have as few errors as possible and if one does occur, it should be able to correct itself. To do this, I will write my code to manage as many different game scenarios as possible so that it will not crash when someone is playing it.

#### Aims

* The game doesn't crash
* The game does not contain any bugs that damage the user experience

### Easy To Learn

The solution should be easy to use and not be over complicated. To do this, I will create simple controls for the game. I will make sure that no more controls are added than are needed in order to keep them as simple as possible for the players.

#### Aims

* Create a list of controls for the game
* Create an in-level guide that helps players learn how to play the game

## Pseudocode for the Game

### Pseudocode for game

This is the basic code I will need in order to create a game in kaboom. This is a good starting point that will allow me to draw a level, create a game scene and paste in a character.&#x20;

```
import kaboom

background colour = "blue"
set window size to (1000,700)

load in Character.pedit as "Character"
load in Floor.pedit as "Floor"
load in Spike V.pedit as "Spike V"
load in Spike H.pedit as "Spike H"

levelconfig = {
    set width to 32
    set height to 32

    "=" set to sprite("Floor"){
        area(),
        origin("bottom")
    }
    
    "+" set to sprite("Spike V"){
        area(),
        origin("bottom")
    }

    "o" set to sprite("Character"){
        area(),
        gravity(),
        origin("bottom")
    }

    "<" set to sprite("Spike H"){
        area(),
        origin("bottom")
    }
}
```

### Pseudocode for a level

This shows the basic layout of code for a kaboom level and game scene. I also paste in the character in the game scene.

```
levels = [
[
  "                                                                       ",
  "                                                         <=============",
  "            +                       +          <==========            ",
  "=========================  ===  =====  =========                       "
  ],
]

create game scene(levelnumber = 0){
    level = addlevel(levels[levelnumber], levelconfig)
    player = spawn in "o" at (1,3) 
}
```
