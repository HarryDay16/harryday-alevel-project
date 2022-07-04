# 2.2.1 Cycle 1

## Design

### Objectives

In this cycle I aim to create a simple level, paste in a character and make it move. I will be doing this in repl.it, and will be using JavaScript with the Kaboom library.&#x20;

* [x] Design a simple level
* [x] Paste in a character
* [x] Make the character automatically move across the screen
* [x] Get keyboard input to make the character jump

### Usability Features

Controls - will be extremely simple and will be using the space bar to make the character jump. This makes the controls very easy to understand so the player doesn't have to spend a long amount of time learning how they work.

Visibility - I want to make each object in the game clearly visible and will be doing this by picking colours that contrast to each other. This will help the player to see each object in the game.

### Key Variables

| Variable Name | Use                   |
| ------------- | --------------------- |
|               | does something useful |

### Pseudocode

```
procedure do_something
    
end procedure
```

## Development

I began by drawing some simple shapes and loading them in so that I could use them later on. I created four simple shapes that I thought would be necessary for my level design: the floor, spikes, the character and the power up.&#x20;

![](<../.gitbook/assets/image (7).png>)

```
loadPedit("Floor", "sprites/Floor.pedit");
loadPedit("Spike", "sprites/Spike.pedit");
loadPedit("Character", "sprites/Character.pedit");
loadPedit("Power Up", "sprites/Power Up.pedit");
```

I then began to design the levels. I had to look up how to do this as I haven't  used this library  that much, so I had forgotten how it worked. I saved the level in a list so that I could add more later.

```
const levels = [
[
  "                *                          ++  ",
  "                                  =============",
  "        +                +  +   ===            ",
  "=========  ===  ======  =========              "
  ],
 
]
```

I continued to follow the tutorial I found after doing this, and created the level configuration, which is used to map each icon you have used in your level design to a sprite that you have loaded in. In this case I mapped each "=" to my floor tile, each "+" to my spike and each "\*" to the power up. The tutorial also recommended to paste in the character later on as it would allow you to more easily reference it.

```
const levelconfig = {
  width: 32,
  height: 32,
  pos: vec2(0,400),

  "=": () => [
    sprite("Floor"),
    area(),
    solid(),
    origin("bot")
  ],
  
  "+": () => [
    sprite("Spike"),
    area(),
    origin("bot") 
  ],

  "*": () => [
    sprite("Power Up"),
    area(),
    origin("bot") 
  ] 
}

```

I also added in tags under each object that gave them specific properties. For instance, I added&#x20;

### Challenges

Description of challenges

## Testing

Evidence for testing

### Tests

| Test | Instructions  | What I expect     | What actually happens | Pass/Fail |
| ---- | ------------- | ----------------- | --------------------- | --------- |
| 1    | Run code      | Thing happens     | As expected           | Pass      |
| 2    | Press buttons | Something happens | As expected           | Pass      |

### Evidence
