
# Working Templates for a DAW like workflow using AUM 

These templates require the bellow apps :

- audiobus 
- AUM  
- Xequence 2
- Loopy Pro if recording Audio instrument is necessary in the song. MultiTrack Recorder can be an alternative.  

The template is presented in this video



# How does it work ? 

## On AUM 

The AUM project flows from left (inputs) to right (outputs).  

Here are descriptions based on the [4 MIDI + 2 Audio project](4M\ 2A.audiobuspreset.zip), you can find similar layout on other templates. 
The most complete one is [8 MIDI + 4 Audio project](8M\ 4A.audiobuspreset.zip), one can also start from this one and
remove the unnecessary parts. 

Starting from left to right: 

### Inputs

#### MIDI 

![](src/IMG_0577.PNG) 

The first 2 are the global MIDI inputs for sequencing AUM they are plugged into the sequencer output. In our case this is
Xequence 2 but it can be something else like LK or Hellium AUV3 for instance. A sequencer plugged into the "IN" MIDI bus
must work with different MIDI channel. 

![](src/midiin.001.png)

The "A", "B", "C", ... Midi in will naturally be mapped to instruments in AUM channel named "A", "B" "C" , ... 
The template does not map them for you,  this is most probably the only mapping you have to do. When using an external
keyboard you can use it from Xequence Directly. 

The "Autom. IN" MIDI bus is mapped to the AUM "MIDI Control", this is aimed to handle any automation coming from Xequence 2 to faders, effects, etc... 
this is a separate input line so one can shut it off by disabling or switching it on a side. 


They are 2 MIDI Auv3, both mapped to AUM "MIDI Control :  

- the MidiMixer from 4Pockets 
- the "Q Menu" which is actually a custom Nurack pad widget to navigate trough the project. It is a low profile discreet 
  MIDI AUV3 which shall be all the time here in order to lunch the Mixer from anywhere and move across the project
  (which is faster than going to the bookmark menu). 

 
#### Audio 

Then comes the Audio inputs (2 for this example: "Audio Recorder A" and "Audio Recorder B"). This is where one can fix
the input level and maybe add some effect to be recorded. The loopy pro AUV3 instances (in audio bus)  are receiving these inputs. 

### Instrument Mixer 

Then comes the Instrument driven by MIDI incoming notes from the MIDI bus A, B, C, .... which must be mapped when
loading instruments for the first time. 

![](src/IMG_0578.PNG) 

It is important to keep the pairing (e.g. "A" MIDI in to "A" instrument) because the control of the AUM channel is
mapped by channel. 
For all my projects  A is channel 1, B channel 2, etc ...  

### Audio Mixer 

The recorded clips are comming after and have the name "Audio A", "Audio B", ... 

<img src="src/IMG_0579.PNG" width=300>

The Audios starts from Channel 9, e.g. "Audio A" control channel (volume, pan etc ...) is mapped to channel 9; "Audio B"
to channel 10 and so on. 

### Master 

Two FX buses and the Master is following. Master controls are mapped to Channel 16, FX1 to channel 15 and FX2 to Channel
14. It is on the reverse order so one can add more if not interfering with an Audio line or a MIDI instrument line.  


<img src="src/IMG_0580.PNG" width=400>


### MIDI outputs

Finally this is the MIDI output rooting. This is mainly use when one wants to record MIDI generator AUV3 from AUM to
Xequence 2.  Either you connect the MIDI AUV3 directly to the OUT Midi bus (when recording track by track) or one can
root several MIDI sources to A OUT, B OUT, C OUT, ... when recording  several MIDI track on the Xequence 2 side.       

<img src="src/IMG_0580_2.PNG" width=300>

The individual channel output are actually a small AUV3 call mfxStrip 

<img src="src/IMG_0587.jpg" width=400>

It convert Any MIDI channels to the appropriate channel (1 for A, 2 for B, etc ...). In this way one can plug multi
output MIDI generator without having to care about the used channel by the generator (some does not have the option to
change channels).

The Main OUT is mapped to Xequence Destination as well as the "Autom Rec" which is dedicated to record automation or LFO
for instance. 


## Xequence 2 

The Xequence project is obviously using the same naming, the A instrument is mapped to the Xequence Source Channel 1,
B->2 , C->3, D->4, Audio A->9 , Audio B -> 10, FX2 -> 14, FX1 -> 15, Master -> 16 


![](src/IMG_0582.PNG) 

By default each instrument has its MIDI track. Audio A, Audio B, ...,  FX2, FX1, and  Master MIDI track are there to
record automation.


![](src/IMG_0581.PNG) 

In multitrack record each track receive the Xequence destination source to its corresponding MIDI channel (A->1, B->2,
...). In single track recording the selected track is receiving all the MIDI Xequence is connected with. 

On the configuration side the "virtual source" and MIDI thru shall be turned on. 

MIDI thru allows to be able to work directly from Xequence withtout having to care of mapping things on AUM side. My
keyboard controller is one of the MIDI source of Xequence 2 and when playing it will go to the "A", "B", or "C", etc 
MIDI bus on AUM and the coresponding instrument.

![](src/IMG_0586.PNG)

Also, one has to make sure that the Send Sync is enable on at least one instrument. Which should be the case when
loading the template. 


![](src/IMG_0591.PNG)


## Audio Bus 


### MIDI 

Adding the Xequence 2 somewhere in the MIDI section of audioBus allows to have it in the always shown Audio Bus small
menu and allows to save its state. 


![](src/IMG_0584.PNG)


### AUDIO 

In this example I have two audio lines with two instances of Loopy Pro (AUV3) as clip recorder. Source is coming from
AUM (The "Audio A recorder" and "Audio B  Recorder") and output to AUM as well ("Audio A" and "Audio B" channel on AUM). 


![](src/IMG_0583.PNG)

> **Why does Loopy pro AUV3 are not instantiated directly in AUM ?**

Good question. This is because AUM cannot receive MIDI clock in (at least in 2022-09-07). In other word AUM cannot follow the song position
mastered by Xequence 2. But Audiobus can and can transfer this to Loopy pro AUV3 instances.


Each instances of Loopy pro has several clips (3 linear, 2 loops) for a good start. One can remove or add on the go.
The clips are supposed to represent a take or par of the song for the same audio instrument (voice, drum , guitar, ...). 

Clips are placed inside the Loopy Pro Sequencer following the song timeline mastered by Xequence and though Audio Bus.
The Loopy Pro sequencer can be use also to punch in and out a recording by drawing an empty clip inside the sequencer.  

![](src/IMG_0588.PNG)

### CONFIG 

One must unable the MIDI clock in on audiobus, I have also disabled Ableton link so it does not interfere with the MIDI
clock. 



![](src/IMG_0590.PNG)


![](src/IMG_0589.PNG)









