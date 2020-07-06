---
layout: default
title: ETC Ion
grand_parent: Audio, Visual, Lighting
parent: AVL Consoles

---
# ETC Ion (Legacy)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## Cues

### Modes

#### Tracking

When the console is in tracking mode, its default behavior acts as follows: 

_A fixture is programmed into a cue. When the next cue is programmed, any fixtures unmodified between the first and second cue remain at the state they were at in the original cue._

When dealing with intelligent light fixtures, such as moving heads, LED pars, etc, it is recommended to place the board in Tracking mode.

#### Cue-Only

When the console is in cue-only mode, its default behavior acts as follows: 

_A fixture is programmed into a cue. When the next cue is programmed, any fixtures unmodified between the first and second cue are set to their home positions \(most likely turned off\) in the new cue._

### Recording Cues

#### Basic Cues

To record a cue on the Ion or any ETC Eos brand consoles:

* First, set the fixtures to the desired look you would like the cue to have
* When you are ready to record, Press the following buttons:
  * **Record. Cue. \*Number of Cue\*. Enter**

#### **Advanced Cues**

##### **Cue Parts**

You may want to record a single cue, but have different aspects of the scene enter at different times. Breaking a cue into parts is one way to achieve this.

* First, set the fixtures to the desired look you would like the cue part to have
* When you are ready to record, Press the following buttons:
  * **Record. Cue. \*Number of Cue\*. Part. \*Number of Part \(if cue already exists with no parts, use Part 2\). Enter**

If you already have a cue set up and just need to add a single fixture added to a new part, this alternative method works as well:

* Load up the cue you want to modify
* Set the new fixture how you would like it
* **\*Fixture number\*. \(\*If you are only modifying a specific parameter of the fixture, put that here\*\). Copy To. Part. \*Part Number\*.**

#### Cue Numbering Guidance

Cues on an ETC Eos-based system can have numbering equivalent to XXX.XXX. When setting up communication with the rest of the team, it is good to have a defined number sequence guideline to follow to understand where you are at in the performance

| Type of Show | Hundreds | Tens | Ones | . | Tenths | Hundredths | Thousandths |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Theatre | Act | Scene \(Tens\) | Scene \(Ones\) | . | Cue |  |  |
| Church | Service | Song/Section  | Song/Section   | . | Cue  |  |  |
| Dance | Show | Song | Song | . |  |  |  |

There are also cue-specific guidelines for certain events that happen in the show:

| Type of Cue | Hundreds | Tens | Ones | . | Tenths | Hundredths | Thousandths |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Blackout |  |  |  | . |  | 9 | 9 |
| Start of Scene |  |  |  | . | 0 | 1 |  |
| End of Scene |  |  |  | . | 9 |  |  |

### Cue Timing

#### Timing Types

Different aspects of timing can be set for both cues and parts.

| Terminology | Behavior |
| :--- | :--- |
| Up Time | Time for lights in this scene to turn on |
| Down Time | Time for lights in last scene to turn off |
| Dwell Time |  |
| Focus Time | Time for moving lights to move |
| Color Time | Time for color to change |
| Beam Time | Time for any beam options. |

#### Setting Times

* Locate the cue or part you would like to modify timing
* **Cue. \*Cue Number\*. \*Part Number if needed\*. Time \[Up Time\]. \*Number if needed\* Time \[Down Time\]. \*Number if needed\*. etc... Enter.**

### Helpful Knowledge

#### Automark

Automark is enabled by default. This allows intelligent fixtures to set up the next scene while waiting in dark during the current scene. A light must have an intensity of 0 in order for Automark to be enabled for the next cue. You will generally see this when a scene is in blackout, or you have just turned off the intelligent fixtures and will be turning them back on in a future cue with different parameters.

To utilize this feature so you do not have lights moving in weird directions in the middle of a scene, simply program that light to have an intensity of 0 in the cue before you need it. It will then need double the focus time of the cue it is turned off in to focus for the new scene.

Automarked cues are designated with an **M** flag in the playback list.

#### Block

A block will seem like a worthless flag when you are programming, but can be very helpful if/when you need to go back and adjust cues in the future. It's been found that blocks at the start of a scene \(or collection of similar cues\) are the most efficient. The behavior of a BLOCK flag is to stop the inheritance of the tracking-mode at the block. For example, If you have a block on cues 101.00 and 102.00 and need to go back and modify a cyc wash on cue 101.05, the tracking data of 105.05 will only go to 105.999, will be blocked from tracking into 102.00, and not change anything about that already-programmed cue.

Blocked cues are designated with a capital **B** flag in the playback list.

* **Cue. \*Cue Number\*. Block. Enter.**

#### Label

Labels allow you to add documentation to your cues. This level of documentation allows you to have a better understanding of when the cue should go live.

* **Cue. \*Cue Number\*. Label. \*Type note\*. Enter.**

> **Note:** If a cue already has a label you would like to retype, just tap label twice when going to label it, and it will clear the current label

### Editing Cues

#### Known Parameters

* Load up the cue in question
* Open **Blind** Mode
* Select the channel in question
* Modify the known parameter you would like to change
* Select **Live**
* Go to the cue again to see the change.

#### Unknown Parameters

* Load up the cue in question
* Select the channel in question
* Modify the parameter you would like to change
* Re-record the cue
* Go to the cue again to see the change.
* Check the cue before and the cues to the next block or change after to make sure there are no undesired tracks of the changes you made.

### Cue Playback

#### Going Forward

Press the big **GO** button

#### Going Backward

Press the big **STOP/BACK** button twice

## Effects

### Types of Effects

#### Relative \(Linear, Color, Focus\)

Relative effects use math to change parameters relative to their current position by a defined percentage scale. When setting up a relative effect, you define the parameter modified, effect cycle time, percentage scale, etc.

#### Step-Based

Step-based effects are loops of very specific commands where defined channels have defined variables hit defined values on these defined times. These effects are limited only to the fixtures and parameters defined in the effect.

#### Absolute

Absolute effects are loops of very specific commands where, unlike Step-Based effects, only the parameters are defined. This allows you to use this effect on more than just a pre-defined set of fixtures.

### Creating Effects

#### Additional Content

##### ETC Guide on programming Effects

[https://support.etcconnect.com/ETC/Consoles/Eos\_Family/Software\_and\_Programming/Common\_Effects\_and\_How\_to\_Program\_Them\_on\_an\_Eos\_Family\_Console](https://support.etcconnect.com/ETC/Consoles/Eos\_Family/Software\_and\_Programming/Common\_Effects\_and\_How\_to\_Program\_Them\_on\_an\_Eos\_Family\_Console)

### Starting an Effect

* **\*Channel or Group\*. Effect. \*Effect Number\*.**

### Stopping an Effect

* **\*Channel or Group\*. Effect.**

## Submasters

### **Setting A Submaster \(Fader with Green Light\)**

* Locate either a fader with no green light, or a fader with a green light that you want to replace
* Select Blind
* Press **Sub**
* Type the sub number you want
* Press **Enter**
  * If the fader was previously used, type “**1” “Thru” \*max patched address\* “At” “Enter”** to clear out the submaster
* Type the channels you want to use and set them at the value you want
* When you are happy with that submaster, press **Live** and test it.