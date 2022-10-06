# Cycle 2 - Main menu

## Design

### Objectives

* [x] Design a main menu screen that allows you to access the game

### Usability Features

* [x] Ensure that the screen looks good and gives clear instructions as to how to access the level

### Pseudocode for menu

```
if enter key is pressed{
    go to game scene
}
```

## Development

In this cycle I began creating a main menu screen that displays the title and allows you to navigate to the level by clicking on a button. Kaboom allows you to create a menu very easily by using assets that have already been created.&#x20;

```javascript
scene("start", () => {
  add([
    text("Genus Geometriae"),
    pos(vec2(500,200)),
    origin("center"),
  ])
  add([
    text("Click here to Start"),
    origin("center"),
    pos(vec2(500,350)),
    scale(0.5,0.5),
    area(),
    "toStart"
    ])
});
```

I kept the design very basic and functional and added another line of text saying "Click here to start".  This clearly shows the user how to navigate through the menu screen and into the actual game.&#x20;

I positioned and sized both blocks of text using a variety of tags, and added a custom "toStart" tag on the second block of text. This will allow me to reference it later on.

I then began writing the code that would determine if the block of text was clicked on. After researching on the kaboom website I found a function called "onClick" which is able to detect when an object with a specific tag is clicked on. Since I had previously given the text I wanted to be clicked on the "toStart" tag, I just had to pass that string into the function and run the game scene if its conditions were met.

```javascript
onClick("toStart", () => {
    go("game")
    })
```

### Challenges

The biggest challenge I faced here was positioning the text correctly, and it was only through trial and error that I was able to position it correctly.&#x20;

## Testing

| Test | Instructions      | What I expect to happen        | What actually happened | Pass/Fail |
| ---- | ----------------- | ------------------------------ | ---------------------- | --------- |
| 1    | Run the game      | The main menu screen to appear | As expected            | Pass      |
| 2    | Click on the text | The game to begin              | As expected            | Pass      |

### Evidence for Testing

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption><p>The Main menu screen</p></figcaption></figure>
