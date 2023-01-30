# Cycle 8 - Percentage Score

## Design

### Objectives

* [x] Design a timer that increments by one every second
* [x] Implement this timer into the game
* [x] Use this to calculate a percentage score
* [x] Modify the death screen so that the player's score is displayed

### Usability Features

Sizing - The text should be large enough for the user to read.

Positioning - The text should be positioned in the centre of the screen&#x20;

Colour - The text should remain a colour that contrasts with the background, ensuring that it is clearly visible

### Key variables and functions for timer

| Variable/Function name | Use                                                                  |
| ---------------------- | -------------------------------------------------------------------- |
| time                   | Will store a number that will increment by one after a second passes |
| setInterval()          | A function that runs at a set time period.                           |
| console.log()          | Will display the contents to the console                             |

### Pseudocode for timer

```
Every second loop{
  let time = 0
  time++
  console.log(time)
}
```

## Development

### Designing the timer

I initially developed the timing aspect of the game in a completely separate node.js file. This would allow me to get the program to work without having to worry about passing the variables through multiple scenes. Initially I tried to create a function that ran every second, and then added one to a variable every time the function ran. I then printed the variable to check whether the variable had been changed.

<pre class="language-javascript"><code class="lang-javascript"><strong>// timer that increases every second
</strong><strong>let timer = setInterval(() => {
</strong>  let time = 0
  time++
  console.log(time)
},1000)

</code></pre>

### Testing the timer

| Test | Instructions    | What I expect to happen                                         | What actually happened                               | Pass/fail |
| ---- | --------------- | --------------------------------------------------------------- | ---------------------------------------------------- | --------- |
| 1    | Run the program | Every second a the count on the console should increase by one. | Every second the number 1 was printed to the console | Fail      |

### Proof of Testing

#### Test 1

I ran this but it didn't work due to the time variable being reset to zero on every call of the function. The result was the number one being printed every second as shown below.

<figure><img src="../.gitbook/assets/image (1) (1) (2) (2).png" alt=""><figcaption></figcaption></figure>

### Changes due to faults

My idea to fix this was to define the time variable before the function was ran, as I thought that this would mean that the time variable wasn't being redefined on each call of the function.

```javascript
// timer that increases every second
let timer = setInterval((time = 0) => {
  time++
  console.log(time)
},1000)
```

### Testing Second version of the timer

| Test | Instructions    | What I expect to happen                                      | What actually happened                               | Pass/Fail |
| ---- | --------------- | ------------------------------------------------------------ | ---------------------------------------------------- | --------- |
| 2    | Run the program | Every second the count on the console should increase by one | Every second the number 1 was printed to the console | Fail      |

### Proof of testing

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

After running the program I got the same outcome as last time. I realised that this was due to how the function actually worked, and that it wasn't just called once and then the contents repeated every second, but the whole function was called every second. This meant that each cycle was completely unrelated from one another, and that the variable was reset on every cycle.

## Re-Designing the timer

### Key variables and functions for re-designed timer

| Variable/Function name | Use                                       |
| ---------------------- | ----------------------------------------- |
| start                  | stores the start time                     |
| end                    | stores the end time                       |
| console.log()          | prints the calculated time to the console |

#### Pseudocode for re-design

```
If game_start = true {
    let start_time = date.now
}

If game_over = true {
    let end_time = date.now
    let time = end_time - start_time
    print time to screen
}
```

After considering the problem and researching it online I decided to completely re-design the timer as I figured that there must be an easier way to make it. I tried a new method in which I would take two variables and take away one from another to get the final time. To do this I used the Date.now() function which gives the current time in milliseconds. I started by setting a variable called start, and gave it the value of the time at the start of the program being run. I used a simple if statement and then created a new variable called end, giving it the value of the current time. Then I printed the difference between the start time and the time at which the if statement was executed, making sure to round it up to seconds.&#x20;

<pre class="language-javascript"><code class="lang-javascript"><strong>// storing a start time in the variable "start"
</strong><strong>let start = Date.now()
</strong><strong>// user prompt
</strong>let a = prompt("input")
// Run when "1" is the input
if(a == "1"){
  // storing the end time in the variable "end"
  let end = Date.now()
  // printing the difference in start and end times rounded to the nearest second
  console.log(Math.round((end - start)/1000)) 
}
</code></pre>

### Testing the re-designed timer

| Test | Instructions                                     | What I expect to happen                   | What actually happened | Pass/Fail |
| ---- | ------------------------------------------------ | ----------------------------------------- | ---------------------- | --------- |
| 3    | Run the program and then input 1 after 7 seconds | The number 7 should appear on the console | As expected            | Pass      |

### Proof of testing

I ran the program and set a timer on my phone for 7 seconds. I typed in the character "1" and after 7 seconds pressed enter. As you can see below the number "7" was printed onto the screen so my program ran successfully.

<figure><img src="../.gitbook/assets/image (1) (1) (3).png" alt=""><figcaption><p>The time variable printed onto the console</p></figcaption></figure>

##

## Implementing the timer into my game

The next task was to add this feature into my game and show the percentage score at the end of the game. In order to do this I would need to figure out the total time taken to complete the level, and then I would be able to work out the percentage of the level that the player had completed. I did this by adding the timer into my game and then printing the time it took to play through the level. This would give me a far more accurate result than timing on a separate device.&#x20;

```javascript
// Storing the start time as a constant
const startTime = Date.now()
```

Firstly I wrote this line of code into the game scene. This is so the start time is set as soon as the game scene begins, and not while the player is still in the menu.&#x20;

After this I needed to find the conditions where I would create the endTime variable. I simplified my previous code by making a new "kill" tag and adding it to the spike and enemy configurations. This would allow me to remove all the individual functions I had for each sprite, and instead create one function that would work for them all.

```javascript
// Enemy Configuration
  "x": () => [
    sprite("Slime"),
    area(),
    body(),
    origin("bot"),
    scale(3,3),
    "Kill",
    "Move"
  ],
  // Vertical Spike Configuration
  "+": () => [
    sprite("Spike V"),
    area(),
    origin("bot"),
    "Kill"
  ],
  // Horizontal Spike Configuration
  "<": () => [
    sprite("Spike H"),
    area(),
    origin("bot"),
    "Kill"
  ],
```

```javascript
// Detection for collisions with any object with "Kill" tag
  player.onCollide("Kill", () => {
    go("death")
  })
```

Since there are now two separate conditions that are able to send the player to the death scene I had to repeat the same lines of code for both conditions. I also decided to calculate the overall time here so that I would only have to pass one variable through to the next scene. I then modified the go() function, passing through the time variable so that it could be used in the death scene.

```javascript
 // Collisions with any object with "Kill" tag
  player.onCollide("Kill", () => {
    // Defining the time when the player dies
    const endTime = Date.now() 
    // Calculating the overall time 
    const time = (endTime - startTime)
    // Passing in the time variable so that the percentage score can be calculated 
    go("death",time)
  })
  // Detection for falling off the screen
  onUpdate(() => {
  if(player.pos.y > 700){
    // Defining the time when the player dies
    const endTime = Date.now() 
    // Calculating the overall time 
    const time = (endTime - startTime)
    // Passing in the time constant so that the percentage score can be calculated 
    go("death",time)
    }
  })

```

As well as this I also added the same line of code after the player collides with the portal. This will allow me to find out the total time the level takes to complete later on.&#x20;

```javascript
// Detection for portal collision
player.onCollide("Win", () =>{
    // storing end time as a constant
    const endTime = Date.now() 
    // calculating the overall time
    const time = (endTime - startTime)
    // passing in the time constant
    go("win",time)
  })
})
```

My next task was to find out how long the level took to complete. In order to do this I modified the win screen and instead of displaying a message after the game had been completed I displayed the time it had taken.&#x20;

```javascript
scene("win", (time) => {
  add([
    text(time, { size: 24 }),
    pos(vec2(500, 350)),
    origin("center"),
    color(255, 255, 255),
  ]);
```

Then after playing through the entire level and reaching the portal at the end this screen appeared with the time taken to complete the level. The value was 31382.

<figure><img src="../.gitbook/assets/image (24) (1).png" alt=""><figcaption><p>The time taken to complete the level</p></figcaption></figure>

After this I changed the win scene back to how it was and removed the code I had previously added in the collision with the "win" tag.&#x20;

I then moved over to the death scene where I was able to calculate the percentage score of the player.

```javascript
// calculating the percentage score
let score = Math.round((time/31382)*100)
```

This line of code divides the time the player spent in the level by the total time it takes to complete the level, multiplies it by 100 and then rounds it to the nearest integer. This tells us the amount of the level that had been completed as a percentage.&#x20;

Finally I made a modification to the message that is shown in the death screen, and added in the score so that it was clearly visible for the player to see.&#x20;

```javascript
// Adding in text displaying the percentage score and giving a prompt. 
  add([
    text( score+"%"+"\nPress enter to return to the main menu", { size: 35 }),
    pos(vec2(500, 350)),
    origin("center"),
    color(255, 255, 255),
  ]);
```

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption><p>The death screen after competing 7% of the level</p></figcaption></figure>

### Challenges

Throughout this cycle I faced a lot of challenges, and was constantly problem solving and figuring out different ways to approach the problem. The biggest challenge was in designing the timer itself. After spending lots of time trying to figure out how to get my timer to function properly I decided to completely re-design it, and figured out a new way to solve the problem at hand. This payed off very well in the end, as I managed to design a timer that worked well and was easy to implement into my game.&#x20;

## Testing

| Test | Instructions                                     | What I expect to happen                                        | What actually happened | Pass/fail |
| ---- | ------------------------------------------------ | -------------------------------------------------------------- | ---------------------- | --------- |
| 4    | Collide with a Spike and reach the death screen. | A message to appear with the players score positioned above it | As expected            | Pass      |

### Evidence of Testing

#### Test 4

Test 4 was successful, and after colliding with a spike at the beginning of the game the death screen appeared and the percentage score is shown.

<figure><img src="../.gitbook/assets/image (6) (2) (1).png" alt=""><figcaption></figcaption></figure>
