---
layout: default
title: Lighting
grand_parent: Audio, Visual, Lighting
parent: AVL Concepts
has_children: true
---
# Lighting Concepts
{:toc}

## Vernacular
{:toc}

| DMX | IP/Tech Equivelent |
| :---: | :---: |
| Dimmer | Physical Relay or Potentiometer |
| Fixture | Device/Client |
| Intelligent Fixture | Device with multiple NIC's |
| DMX Address \(1-512\) and Channel | IP Address \(10.0.0.x\) |
| Universe | Subnet \(10.0.x.0\) |
| Repeater/Splitter/Gateway | Switch |
| Console | Server/Router |
| Dip Switches | Binary Static Assignment |


## DMX and Networking
{:toc}

### DMX \(DMX512\)
{:toc}

Digital Multiplex \(DMX\) is the standard communication network for architectural and stage lighting and effects. This network is used to communicate between lighting consoles, dimmers, and intelligent lighting fixtures. This network utilizes XLR5 \(5-pin\) and in some cases XLR3 \(3-pin\). While XLR3 is not permitted in DMX compliance, it is still commonly available on a massive amount of light fixtures. If you plan to use XLR3 in your DMX environment, ensure you are not plugging a light into an audio channel as that can cause significant damage to the fixture.

### The Network
{:toc}

If you have a basic understanding of IP networks, DMX will be easy to understand. Contrary to IP using 256 addresses and not being able to use address 1 \(gateway\) or 255 \(broadcast\), DMX uses 512 addresses per universe, and you can use all address 1 through 512. Fixtures use one address per action. For dimmers, this would be one address, intensity from 0 to 255. For intelligent lights and effects, this may be two, four, seven, sixteen, or fifty-two, etc. addresses per fixture. When you set addresses for fixtures, you only set the starting address and calculate what the last address of the device is based on the mode it is in – how many channels are being actively used.

#### Dip Switch Addressing
{:toc}

Some fixtures require you to set the address of the light using binary dip switches. On the device there would be 9 dip switches, usually with an identifier of 1-9. You set the address by playing the price is right rules and using addition. Find the closest value without going over, then add up the rest of the values to land on the correct address. An address of 4 would have dip switch 3 at the on position, and all other dip switches at the off position. A value of 511 would have all in the on position. There are also numerous online DMX dip switch calculators online that can assist with finding the correct configuration. You can assign channels individually to fixtures, or group fixtures together with the same address.

![](/assets/avl-dip.jpg)

#### Change Behavior Examples
{:toc}

![](/assets/avl-dmx-change.png)


## Techniques
{:toc}

### Three-Point Lighting
{:toc}

### Color Theory
{:toc}
