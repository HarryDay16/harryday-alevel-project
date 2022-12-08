# Cycle 8 - Percentage Score

## Design

### Objectives

* [x] I will be adding in a percentage sore at the death screen so the player can see how far through the level they got

### Usability Features

Sizing - The text should be large enough for the user to read.

### Pseudocode

<pre><code>If game_start = true {
<strong>    let start_time = date.now
</strong>}

If game_over = true {
    let end_time = date.now
    let time = end_time - start_time
    print time to screen
}
</code></pre>

## Development

### Designing the timer

I initially developed the timing aspect of the game in a completely separate node.js file. This would allow me to get the program to work without having to worry about passing the variables through multiple scenes. Initially I tried to create a function that ran every second, and then added one to a variable every time the function ran. I then printed the variable to check whether the variable had been changed.

```javascript
let timer = setInterval(() => {
  let time = 0
  time++
  console.log(time)
},1000)

```

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

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

After running the program I got the same outcome as last time. I realised that this was due to how the function actually worked, and that it wasn't just called once and then the contents repeated every second, but the whole function was called every second. This meant that each cycle was completely unrelated from one another, and that the variable was reset on every cycle.

### Re-Designing the timer

After considering the problem and researching it online I decided to completely re-design the timer as I figured that there must be an easier way to make it. I tried a new method in which I would take two variables and take away one from another to get the final time. To do this I used to Date.now() function which gives the current time in milliseconds. I started by setting a variable called start, and gave it the value of the time at the start of the program being run. I used a simple if statement and then created a new variable called end, giving it the value of the current time. Then I printed the difference between the start time and the time at which the if statement was executed, making sure to round it up to seconds.&#x20;

```javascript
let start = Date.now()
let a = prompt("input")
if(a == "1"){
  let end = Date.now()
  console.log(Math.round((end - start)/1000)) 
}
```

I ran this and set a timer on my phone for 7 seconds. I typed in the character "1" and after 7 seconds pressed enter. As you can see below the number "7" was printed onto the screen so my program ran successfully.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>The time variable printed onto the console</p></figcaption></figure>

### Implementing the timer into my game

The next task was to add this feature into my game and show the percentage score at the end of the game. In order to do this I would need to figure out the total time taken to complete the level, and then I would be able to work out the percentage of the level that the player had completed. I did this by adding the timer into my game and then printing the time it took to play through the level. This would give me a far more accurate result than timing on a separate device.&#x20;

```javascript
const startTime = Date.now()
```

Firstly I wrote this line of code into the game scene. This is so the start time is set as soon as the game scene begins, and not while the player is still in the menu.&#x20;

After this I needed to find the conditions where I would create the endTime variable. since there are two separate conditions that are able to send the player to the death scene I had to repeat the same lines of code for both conditions. I also decided to calculate the overall time here so that I would only have to pass one variable through to the next scene. I then modified the go() function, passing through the time variable so that it could be used in the death scene.

```javascript
 player.onCollide("Kill", () => {
    const endTime = Date.now() 
    const time = (endTime - startTime)
    go("death",time)
  })

  onUpdate(() => {
  if(player.pos.y > 700){
    const endTime = Date.now() 
    const time = (endTime - startTime)
    go("death",time)
    }
  })

```

As well as this I also added the same line of code after the player collides with the portal. This will allow me to find out the total time the level takes to complete later on.&#x20;

```javascript
player.onCollide("Win", () =>{
    const endTime = Date.now() 
    const time = (endTime - startTime)
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

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption><p>The time taken to complete the level</p></figcaption></figure>

After this I changed the win scene back to how it was and removed the code I had previously added in the collision with the "win" tag.&#x20;

I then moved over to the death scene where I was able to calculate the percentage score of the player.

```javascript
let score = Math.round((time/31382)*100)
```

This line of code divides the time the player spent in the level by the total time it takes to complete the level, multiplies it by 100 and then rounds it to the nearest integer. This tells us the amount of the level that had been completed as a percentage.&#x20;

Finally I made a modification to the message that is shown in the death screen, and added in the score so that it was clearly visible for the player to see.&#x20;

```javascript
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

| Test | Instructions                                                      | What I expect to happen                                                               | What actually happened                  | Pass/fail |
| ---- | ----------------------------------------------------------------- | ------------------------------------------------------------------------------------- | --------------------------------------- | --------- |
| 1    | Run the timer program                                             | Every second a number will be printed onto the console, increasing by one every time. | The number 1 was printed every second.  | Fail      |
| 2    | Run the timer program and input the character "1" after 7 seconds | The number 7 to be printed onto the console                                           | As expected                             | Pass      |
| 3    | Collide with a Spike and reach the death screen.                  | A message to appear with the players score positioned above it                        | As expected                             | Pass      |

### Evidence of Testing

After testing my initial timer program I realised that its design would not work since I couldn't continuously change a variable without redefining it. Therefore I completely re-designed the timer, attempting to solve the issue in a new way.&#x20;

<figure><img src="../.gitbook/assets/image (8) (2).png" alt=""><figcaption></figcaption></figure>

My second attempt to create a timer was successful, and my program successfully printed the time it took for me to enter the character "1" .&#x20;

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

My final test was also successful, and after implementing the timer into my actual game the percentage score was displayed on the death screen.&#x20;

<figure><img src="../.gitbook/assets/image (6) (2).png" alt=""><figcaption></figcaption></figure>
