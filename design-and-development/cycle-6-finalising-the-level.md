# Cycle 6 - Finalising the level

Design

### Objectives

* [x] Finish designing the entire level and play through it to ensure it is beatable

### Usability Features

* [x] Ensure that the level is beatable but still challenging enough so that it isn't boring

## Development

For this stage of development I will be creating a much longer level, and it will include both spikes and enemies. The level I had created at the start was very simple and short, and the second level I created was only meant to be used for testing the enemies. Initially I tried to create this level in the same way I had done before, but due to the level becoming much longer it became hard to design it in the small repl.it window. This was because the code would go onto new lines making the code look very messy and unorganised.

<figure><img src="../.gitbook/assets/image (2) (3).png" alt=""><figcaption><p>Screenshot of level development in repl.it</p></figcaption></figure>

Instead I designed the level in notepad, which is a simple text editor. Notepad allows you to scroll left and right as far as you need, so was perfect for designing a longer level since it wouldn't skip any lines. I was then able to finish designing the level much more easier as I could visualise the level better and understand where I was placing each game object.

The first section of the level is pretty simple, with only spikes and a gap in the floor for the player to avoid. I tried to create some variation in the way I laid out the spikes as I think this will make it more fun to play.&#x20;

<figure><img src="../.gitbook/assets/image (1) (5).png" alt=""><figcaption></figcaption></figure>

```javascript
levels = [ 
[
  "                                                                      ",
  "                                                                      ",
  "                                                                      ",
  "                                                                      ",
  "                                                                      ",
  "                                 +                              <=====",
  "              +++      ++       <=      +++           <===========    ",
  "==================================================    <=              "
  ],
  ]
```

After this section I began to experiment with the assets I had available, creating some more unique elements and interesting spike combinations. This will aim to throw the player off and also introduces them to some more unexpected elements.

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

<pre class="language-javascript"><code class="lang-javascript"><strong>levels = [ 
</strong>[
 "                                                       +++      ",
 "                                                 &#x3C;============= ",
 "                                                 &#x3C;=             ",
 "                                         &#x3C;=========             ",
 "    ++     +       +        +      &#x3C;=======                     ",
 "================+++=       &#x3C;=========                           ",
 "              ==============                                    ",
 " 								  "
  ]
</code></pre>

The next section increases in difficulty yet again, and introduces the enemies. I placed these at uneven intervals across the platforms so it is harder for the player to time the jumps correctly. I then threw in some spikes and a gap in the floor just to add in some variety. This will definitely be one of the most challenging sections of the level, and will require the player to time 9 jumps correctly in order to progress.

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

```javascript
levels = [ 
[
"       x           x                  x  ++                      +                                     ",
"===========================================                  x  <=                   x             x   ",
"                                          ===========================   ===============================",
"                                                                                                       ",
"                                                                                                       ",
"                                                                                                       ",
"                                                                                                       ",
"													"                                                                                   ],
  ]
```

&#x20;The final section is shown below and includes a very challenging jump just before the end. I have included a new character "0" which I will later map to a portal. If the player makes contact with the portal the game will end and they will be sent to a win screen.

<figure><img src="../.gitbook/assets/image (1) (3).png" alt=""><figcaption></figcaption></figure>

```javascript
levels = [ 
[
"  +                                                      ",
" <=         +                                            ",
"===         =                 +            0             ",
"  ===========         +++    <=                          ",
"           =================================             ",
"                                                         ",
"                                                         ",
"						          "                                                                                                                                                                                                                                               
  ],
  ]
```

The final code for the level is shown below, and I think it will be a good difficulty while being fun to play. I also think that it is a sufficient length and the player won't feel that it was too short.&#x20;

```javascript
levels = [ 
"                                                                                                                          +++                  x         x              x  ++                      +                                           +                                                       ",
  "                                                                                                                    <========================================================                  x  <=                     x             x      <=         +                                             ",
  "                                                                                                                    <=                                                      ===========================   ======================================         =                 +            0              ",
  "                                                                                                            <=========                                                                                                                         ===========         +++    <=                           ",
  "                                                                       ++     +       +        +      <=======                                                                                                                                           =================================             ",
  "                                 +                              <==================+++=       <=========                                                                                                                                                                                               ",
  "              +++      ++       <=      +++           <===========                ==============                                                                                                                                                                                                       ",
  "==================================================    <=																													          "                                                                                                                                                                                                                                               
  ]
```

### Challenges

Designing this level was definitely challenging as it required me to visualise the level and come up with creative ideas. It was also quite a time consuming process as I had to manually place in every&#x20;

## Testing

To test the level more easily I added another empty array into the levels array. I split the level up into each of the 4 smaller sections and tested them all independently, copying and pasting each section into this new array.

By testing the level in this way it meant that I didn't have to keep on playing through the entire level to test a new section, and that I was able to design the level far more efficiently.

| Test | Instructions  | What I expect to happen                                                                        | What actually happened | Pass/Fail |
| ---- | ------------- | ---------------------------------------------------------------------------------------------- | ---------------------- | --------- |
| 1    | Run section 1 | There is enough space between each obstacle so that it is possible to get through the section. | As expected            | Pass      |
| 2    | Run section 2 | There is enough space between each obstacle so that it is possible to get through the section  | As expected            | Pass      |
| 3    | Run section 3 | There is enough space between each obstacle so that it is possible to get through the section. | As expected            | Pass      |
| 4    | Run section 4 | There is enough space between each obstacle so that it is possible to get through the section. | As expected            | Pass      |

### Evidence of testing

#### Section 1

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

This section was quite simple to complete and I think it introduces the player to the games mechanics nicely. The test was passed and it is possible to complete all of the jumps.

#### Section 2

<figure><img src="../.gitbook/assets/image (5) (3).png" alt=""><figcaption></figcaption></figure>

Once again I was able to reach the end of the section successfully and I can confirm that all of the jumps are possible.

#### Section 3

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

I was able to reach the end of this section, however it took me a few attempts. The enemies add more of a challenge to the game and require the jumps to be timed more precisely.&#x20;

#### Section 4

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Here you can see that I was able to reach the end of the final section. The last jump was challenging, however it is definitely possible so the test was passed.

<figure><img src="../.gitbook/assets/image (2) (1) (3).png" alt=""><figcaption><p>Image displaying the character stationary and pushed up against the obstacle</p></figcaption></figure>

However, I did find an issue in this section of the game. Here you can see that the player is completely still and pushed up against the side of the obstacle. The issue here was that the character was not actually touching the spike on top of the black wall, meaning that the death screen didn't appear when they came into contact.
