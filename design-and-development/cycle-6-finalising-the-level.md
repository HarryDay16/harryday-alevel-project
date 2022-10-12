# Cycle 6 - Finalising the level

## Design

### Objectives

* [x] Finish designing the entire level and play through it to ensure it is beatable

### Usability Features

* [x] Ensure that the level is beatable but still challenging enough so that it isn't boring

## Development

For this stage of development I began by designing the rest of the level. The level I had created at the start was very simple and short, and didn't have a win screen at the end. I tried to create the rest of the level in the same way as before, but due to the level becoming much longer it became hard to design it in the small window. This was because the code would go onto new lines making the code look very messy and unorganised.

<figure><img src="../.gitbook/assets/image (2) (3).png" alt=""><figcaption><p>Screenshot of level development in repl.it</p></figcaption></figure>

Instead I copied and pasted my code for the level and put it into notepad, which is a simple text editor. I was then able to finish designing the level much more easier as I could visualise the level better and understand where I was placing each game object.

To create the final version of my level took multiple attempts and tests to see how easy the level was to beat and whether or not some areas were impossible to complete. I also wanted it to be a decent length so that the game felt more complete and less of a half done project.&#x20;

<figure><img src="../.gitbook/assets/image (5) (1) (3).png" alt=""><figcaption><p>Screenshot of the final level in notepad</p></figcaption></figure>

The final level is shown above and after playing through it multiple times I felt that it was a good difficulty and had some fun elements in it. The entire level lasts a little over thirty seconds which I feel is a sufficient length for a single level.&#x20;

I have also added a new character at the end of the level. This is the "0" and I intend on mapping it to a portal image that if hit by the player results in a win screen appearing.&#x20;

### Challenges

Designing this level was definitely challenging as it required me to make lots of small changes after each test run to ensure that the level could still be completed.

## Testing

To test the level more easily I added another empty array into the levels array. I designed 4 smaller sections and tested them all independently, copying and pasting each section into this new array.

By testing the level in this way it meant that I didn't have to keep on playing through the entire level to test a new section, and that I was able to design the level far more efficiently.

| Test | Instructions    | What I expect to happen                                                                      | What actually happened                                                                                                                                               | Pass/Fail |
| ---- | --------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| 1    | Run section one | There is enough space between each obstacle so that it is possible to get through the level. | As expected                                                                                                                                                          | Pass      |
| 2    | Run section 2   | There is enough space between each obstacle so that it is possible to get through the level. | My first design did not work as expected and one of the enemies came too close to the spikes, making it impossible to clear the jump.                                | Fail      |
| 3    | Run section 2   | There is enough space between each obstacle so that it is possible to get through the level. | As expected                                                                                                                                                          | Pass      |
| 4    | Run section 3   | There is enough space between each obstacle so that it is possible to get through the level. | As expected                                                                                                                                                          | Pass      |
| 5    | Run section 4   | There is enough space between each obstacle so that it is possible to get through the level. | Once again there was an issue with how the enemies interacted with the spikes, making it impossible to clear some of the jumps                                       | Fail      |
| 6    | Run section 4   | There is enough space between each obstacle so that it is possible to get through the level. | All of the obstacles could be completed, however there was a small bug that made the character remain stationary when it came into contact with one of the obstacles | Fail      |
| 7    | Run section 4   | There is enough space between each obstacle so that it is possible to get through the level. | As expected                                                                                                                                                          | Pass      |

### Evidence of testing

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Image displaying the character stationary and pushed up against the obstacle</p></figcaption></figure>

When testing my game I came across a bug. This occurred in the 4th section of my level and shows the character completely still and pushed up against the side of the obstacle. The issue here was that the character was not actually touching the spike on top of the black wall, meaning that the death screen didn't appear when they came into contact.&#x20;
