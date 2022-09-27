# Cycle 5 - Main menu

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

In this cycle I began creating a main menu screen that displays the title and allows you to navigate to the level by clicking on a button.&#x20;

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
    add([
      text("Tutorial"),
      origin("center"),
      pos(vec2(500,450)),
      scale(0.5,0.5),
      area(),
      "tutorial"
    ])

    
    
    onClick("toStart", () => {
    go("game")
    })
    onClick("tutorial", () => {
      go("tutorial")
    })
  
});javas
```
