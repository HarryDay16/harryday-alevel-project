# Cycle 1 - Drawing the level

## Design

### Objectives

In this cycle I aim to create a simple level, paste in a character and make it move. I will be doing this in repl.it, and will be using JavaScript with the Kaboom library.&#x20;

* [x] Design a simple level
* [x] Paste in a character

### Usability Features

Visibility - I want to make each object in the game clearly visible and will be doing this by picking colours that contrast to each other. This will help the player to see each object in the game more easily.

### Pseudocode

The pseudocode for the level configuration is below

```
levelconfig = {
set width to 32
set height to 32

"=" set to sprite("Floor")

"+" set to sprite("Spike V")

"o" set to sprite("Character")

"*" set to sprite("Power Up")

"<" set to sprite("Spike H")
}

```

## Development

I began by drawing some simple shapes and loading them in so that I could use them later on. I created four simple shapes that I thought would be necessary for my level design: the floor, spikes, the character and the power up.&#x20;

![](<../.gitbook/assets/image (7).png>)

```
loadPedit("Floor", "sprites/Floor.pedit");
loadPedit("Spike V", "sprites/Spike V.pedit");
loadPedit("Spike H", "sprites/Spike H.pedit");
loadPedit("Character", "sprites/Character.pedit");
loadPedit("Power Up", "sprites/Power Up.pedit");
```

I then began to design the levels. I had to look up how to do this as I haven't  used this library  that much, so I had forgotten how it worked. I saved the level in a list so that I could add more later.

```
const levels = [
[
  "                                                                       ",
  "                                                         <=============",
  "            +                       +          <==========            ",
  "=========================  ===  =====  =========                       "
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

I also added in tags under each object that gives them specific properties.&#x20;

While I was doing this I also modified the size of the game window and made the background blue. This made the game much clearer and nicer to look at, and was very simple to do.

```
kaboom({
  background: [0, 34, 255],
  width: 1000,
  height: 700,
})
```

After the level was completely designed I added the level to a game scene and pasted in the character at the start of the level. The use of game scenes will allow me to more easily add more levels later on as I can save each level as its own game scene and run it when the user clicks on it in the menu.

### Challenges

The main challenge I faced here was trying to re-learn how the kaboom library actually works, and understanding what each section of code does. I used both the kaboom website and a kaboom tutorial to help me with this which really helped me in understanding the basics of kaboom.

## Testing

### Tests

| Test | Instructions | What I expect                          | What actually happens | Pass/Fail |
| ---- | ------------ | -------------------------------------- | --------------------- | --------- |
| 1    | Run code     | The level and the character to appear. | As expected           | Pass      |

### Evidence

![This image shows the sprite stationary with the level also visible](<../.gitbook/assets/image (9).png>)
