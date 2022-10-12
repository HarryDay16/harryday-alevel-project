# Cycle 2 - Main menu

## Design

### Objectives

* [x] Design a main menu screen that allows you to access the game

### Usability Features

Ensure that the screen looks good and gives clear instructions as to how to access the level

### Pseudocode for menu

```
create start scene {
    add([ 
        text("Genus Geometriae")
        ])
    add([ 
        text("Click Here To Start"),
        area()
        On click(go("game))
        ]) 
}
```

## Development

In this cycle I began creating a main menu screen that displays the title and allows you to navigate to the level by clicking on a button. Kaboom allows you to create a menu very easily by using scenes. You can create a variety of different scenes and navigate from scene to scene, allowing for different levels and menus to be created very simply.

I began by creating a "start" scene. In this scene I added the title of the game as well as another line of text saying "Click here to start".  I kept this design simple as I want the user to not waste time navigating through the menus, which can sometimes get frustrating.

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

I positioned and sized both blocks of text using a variety of tags, and added a custom "toStart" tag on the second block of text. This will allow me to reference it later on when I want to make it into a button.

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption><p>The menu screen</p></figcaption></figure>

I then began writing the code that would determine if the block of text was clicked on. After researching on the kaboom website I found a function called "onClick" which is able to detect when an object with a specific tag is clicked on. Since I had previously given the text I wanted to be clicked on the "toStart" tag, I just had to pass that string into the function and run the game scene if its conditions were met.

```javascript
onClick("toStart", () => {
    go("game")
    })
```

After running this it worked perfectly, and the game screen appeared once the text was clicked on.

### Challenges

The biggest challenge I faced here was positioning the text correctly, and it was only through trial and error that I was able to get it to the right size and shape. I set the origin of the text to the center and used the screen dimensions (1000,700) in order to make the process easier, however i still took 4 or 5 attempts until I got the menu to look how I wanted it to.

## Testing

| Test | Instructions                        | What I expect to happen        | What actually happened | Pass/Fail |
| ---- | ----------------------------------- | ------------------------------ | ---------------------- | --------- |
| 1    | Run the game                        | The main menu screen to appear | As expected            | Pass      |
| 2    | Click on the text                   | The game to begin              | As expected            | Pass      |
| 3    | Click around the text but not on it | The game should not begin      | As expected            | Pass      |

### Evidence for Testing

#### Test 1

<figure><img src="../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>

After running the game the menu screen appeared as expected. This test was therefore a success.

#### Test 2

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

After clicking on the text the game scene appeared. This test was also a success.

#### Test 3

I added this test to ensure that the buttons hitbox wasn't too large and that it functioned correctly. I tried clicking everywhere around the button and the game scene never appeared. Therefore this test was also successful.
