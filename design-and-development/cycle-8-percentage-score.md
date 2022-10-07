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
}</code></pre>

## Development

I initially developed the timing aspect of the game in a completely separate node.js file. This would allow me to get the program to work without having to worry about passing the variables through multiple scenes. Initially I tried to create a function that ran every second, and then added one to a variable every time the function ran. I then printed the variable to check whether the variable had been changed.

```javascript
let timer = setInterval(() => {
  let time = 0
  time++
  console.log(time)
},1000)

```

I ran this but it didn't work due to the time variable being reset to zero on every call of the function. The result was the number one being printed every second as shown below.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

My idea to fix this was to define the time variable before the function was ran, as I thought that this would mean that the time variable wasn't being redefined on each call of the function.

```javascript
let timer = setInterval((time = 0) => {
  time++
  console.log(time)
},1000)
```

However, I got the same outcome from running this. I realised that this was due to how the function actually worked, and that it wasn't just called once and then the contents repeated every second, but the whole function was called every second. This meant that each cycle was completely unrelated from one another. At this point I did some research and found another way to create a timer.&#x20;

