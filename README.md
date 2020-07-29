# Practical Scripting with Python
## UNO Summer Techademy

### EarSketch
EarSketch is a tool that allows us to create music using python (or javascript) coding.
- [EarSketch Website](http://earsketch.gatech.edu/landing/#/)

Once there, click **get started**. You can create an account but you don't have to do that to start programming, only if you want to save your work.

### Your first song
- Create a new script using Python. You can give it any name you would like.
- You'll want to spend some time listening to the existing samples.

#### fitMedia(sample, track, startMeasure, stopMeasure)
- The sample is anything from the sound collection.
- Tracks should not overlap, have each sound in it's own track beginning with 1.
- start/stop measures will determine when in the song the sound is played.

```
bass = YG_FUNK_BASS_1
guitar = YG_FUNK_FUNK_GUITAR_1

fitMedia(bass, 1, 1, 10)    #bass on track 1, measures 1 - 10
fitMedia(guitar, 2, 3, 8)   #guitar on track2, measures 3 - 8
```

### Sound Effects
There are many effects in EarSketch here is a list of what you can do:
- BANDPASS
- CHORUS
- COMPRESSOR
- DELAY
- DISTORTION
- EQ3BAND
- FILTER
- FLANGER
- PAN
- PHASER
- PITCHSHIFT
- REVERB
- RINGMOD
- TREMOLO
- VOLUME
- WAH

With each of the effects, you have the following command:
**setEffect(track, effect, parameter, value)**
- Track: Which track are we applying this effect to?
- Effect: Which effect are we using (from the above list)
- Parameter: Each effect has different parameters that can be changed.
  - For example, in REVERB we have REVERB_TIME, REVERB_DAMPFREQ, MIX
- Value: What value should we set to this parameter?

#### Example:
```
setEffect(1, VOLUME, GAIN, -5.0) #Turn down volume by 5 units on track 1.
setEffect(2, REVERB, REVERB_TIME, 1000.0) #Add a reverb effect to track 2, set the time to 1000 ms (1 second)
```
### Envelopes with setEffect
The setEffect() function takes a variable number of arguments. Its full set of arguments is listed below.
- trackNumber
- effectName
- effectParameter
- effectStartValue
- effectStartLocation
- effectEndValue
- effectEndLocation

#### Example
```
#Music
fitMedia(ELECTRO_ANALOGUE_LEAD_012, 1, 1, 9)
# Makes an effect ramp between measures 1 and 3, moving from -60dB to 0dB
setEffect(1, VOLUME, GAIN, -60, 1, 0, 3)
```

### MakeBeat
In EarSketch, we can create our own beat patterns. You will want to use the sounds from the MAKEBEAT artist. You define how a beat will be shaped with a few different commands.
A zero (0) is the hit of a beat.
A plus sign (+) sustains the sound
A minus sign (-) cuts off the sound.

Example beat on 1 & 3 of a four beat measure
```
bassBeat = "0+++--0+0+++----"
```

Then we add a beat sound using the makeBeat command.
**makeBeat(sound, track, measure, pattern)**
- Sound: What is the sound file that will be played for each beat sound
  - Use sounds from the MakeBeat artist.
- Track: What track of your song has the beat sounds
- Measure: We only apply the MakeBeats one measure at a time
- Pattern: What beat pattern are we using?

#### Example
```
bassDrum = OS_LOWTOM01
bassBeat = "0+++--0+0+++----"
makeBeat(bassDrum, 3, 1, bassBeat)
```

Since this only creates one measure of beat, we may want to loop the command
```
for count in range(1, 9):
  makeBeat(bassDrum, 3, count, bassBeat)
```

More complex example:
```
bass = OS_LOWTOM01
snare = OS_SNARE01
hiOpen = OS_OPENHAT01
hiClosed = OS_CLOSEDHAT01
bassBeat = "0+++--0+0+++----"
snareBeat = "----0+++-0+-0+++"
running = "0+0+0+0+0+0+0+0+"
fillBass = "0+++0+++0+0+0+0+"
fillSnare = "0+++0+++0+0+0000"

for measure in range(1, 9):
 if measure % 4 != 0:
  makeBeat(hiClosed, 1, measure, running)
  makeBeat(snare, 2, measure, snareBeat)
  makeBeat(bass, 3, measure, bassBeat)
 else:
  makeBeat(hiClosed, 1, measure, running)
  makeBeat(snare, 2, measure, fillSnare)
  makeBeat(bass, 3, measure, fillBass)
```

## End of course survey
Please take [This Survey](https://docs.google.com/forms/d/1brzBg0H_rl3MUJVzonJR5nFNKazMsT64aFyKTXKVUGQ/edit) about
