---
layout: default
title: GRLevel 3
parent: Weather
---

# GRLevel 3
{: .no_toc }

Level 3 Radar Data Visualizer
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---

## Installation and Updates

* Download the [latest version of GRLevel3](http://grlevelx.com/downloads/grlevel3_2_setup.exe)
* If you are updating, [use the update link.](http://grlevelx.com/downloads/grlevel3_2_update.exe)

## License

* [Purchase a license key from GRLexelX](http://grlevelx.com/grlevel3_2/) if you don't already have one.
* Open GRLevel3
* Select Help
* Select About
* Select Register
* Enter the license key provided.

## Set Default Radar

* Open GRLevel3
* Select Site
* Select Settings
* Select Settings
* Select Change
* Scroll down and select the site closest to you
* Select OK
* Select OK again
* Close and reopen GRLevel3

## Color Tables

GRLevel3 defaults to using confusing colors for its storm warning boundaries. In most other products, severe thunderstorm warnings are yellow, but GRLevel3 is red. It is simple to change these to NWS colors.

* Open GRLevel3
* Select View
* Select Warning Settings
* Select NWS Colors
* Select OK

### NWS Warning Colors:

| Color | Warning |
| :--- | :--- |
| Blue | Marine |
| Green | Flood / Flash Flood |
| Yellow | Severe Thunderstorm |
| Red | Tornado |
| Pink | Confirmed Tornado |

## Placefiles

* Placefiles add supplemental information on the radar map.
* Open GRLevel3
* Select Windows
* Select Show Placefile Manager
* Select the + button to add
* Type or pate the link to the placefile information
* Select OK
* Close the placefile manager

## Radar Products

Information and graphics taken from sources referenced below.

### Measurements

**10 Nautical Miles \(nm/knots\) = 11.5 Miles \(mph\)** When ft is displayed in GRLevel3, that shows the minimum height of the beam at that location. The further away from the radar, the higher the minimum value that data can be received from.

### Base Reflectivity \(BR\)

![](/assets/weather-br.jpg)

This looks at the signal response bounced back to the radar at gradual tilts above the horizon, starting at 0.5 degrees. For areas close to the radar, you will need to increase the tilt angle in order to see a better picture of storm intensity. BR is commonly used to detect “hook echoes” that may form into tornadoes.

![](/assets/weather-br1.jpg)

### Composite Reflectivity \(CR\)

![](/assets/weather-cr.PNG)

This looks at the maximum signal received from all tilts captured during the BR runs. This is a great product at measuring storm intensity and hail locations. This will have a slightly exaggerated view from what you may be used to seeing as it may capture anvil \(top of cloud\) and other cloud data.

### Base Velocity \(BV\)

![](/assets/weather-bv1.jpg)

> “This is the velocity of the precipitation either toward or away from the radar \(in a radial direction\). No information about the strength of the precipitation is given. This product is available for just two radar "tilt" angles, 0.5° and 1.45°. Precipitation moving **TOWARD** the radar has negative velocity \[green\]. Precipitation moving **AWAY** from the radar has positive velocity \[red\]. Precipitation moving perpendicular to the radar beam \(in a circle around the radar\) will have a radial velocity of zero, and will be colored grey. The velocity is given in knots \(10 knots = 11.5 mph\)”
>
> -**Wunderground** [**"Understanding Radar"**](https://www.wunderground.com/prepare/understanding-radar)\*\*\*\*

![](/assets/weather-bv.png)

This is used to detect storm rotation. Look for convergence of red and green inside the storm cell.

### Storm Relative Velocity \(SRV\)

![](/assets/weather-srv.PNG)

Similar to Base Velocity, but it subtracts out the mean motion of the storm. With this, it better highlights the motion inside the storm itself.

### Hydrometeor Classification Algorithm

![](/assets/weather-hca.gif)

> “The HCA product attempts to provide a representation of radar echo types \(out of 10 possible echoes - biological, clutter, ice crystals, dry snow, west snow, rain, heavy rain, big drops, graupel, and hail\) in each radar range bin. Uses: HC can provide a first-guess for precipitation type, and it can help point out non-precipitation echoes.”
>
> -**Envirodata.org** [**"Gibson Radar 3 Explanation"**](http://www.envirodata.org/files/gibson_radar_3_explanation.htm#HCA)

### Echo Tops

![](/assets/weather-et.png)

> “The Echo Tops image shows the maximum height of precipitation echoes. The radar will not report echo tops below 5,000 feet or above 70,000 feet, and will only report those tops that are at a reflectivity of 18.5 dBZ or higher. In addition, the radar will not be able to see the tops of some storms very close to the radar. For very tall storms close to the radar, the maximum tilt angle of the radar \(19.5 degrees\) is not high enough to let the radar beam reach the top of the storm. For example, the radar beam at a distance 30 miles from the radar can only see echo tops up to 58,000 feet.
>
> Echo top information is useful for identifying areas of strong thunderstorm updrafts. In addition, a sudden decrease in the echo tops inside a thunderstorm can signal the onset of a downburst--a severe weather event where the thunderstorm downdraft rushes down to the ground at high velocities and causes tornado-intensity wind damage.”
>
> -**Wunderground** [**"Understanding Radar"**](https://www.wunderground.com/prepare/understanding-radar)

### Precipitation type

![](/assets/weather-pt.png)

> “The server generates a new precipitation type data field every five minutes by interpolating the RUC 13km model output. The algorithm is based on the Canadian "Energy" method that has been modified to produce probabilities for rain, freezing rain, sleet, and snow. These probabilities are combined with the radar mosaic in a novel rendering technique to show mixtures of types in real time. Here is an example showing all the precip types overlaid with METAR Present Weather icons."
>
> -**WeatherObservatory.com** [**"GREarth Precip"**](https://www.weatherobservatory.com/grearth-precip.htm)

Example: "The large blue area in the upper-left is all snow, the orange areas are sleet, red areas indicate freezing rain, and the regular reflectivity color area is all rain.”

![](/assets/weather-pt2.png)

To enable this feature, select the T on the main dashboard

### Storm Total Rainfall

![](/assets/weather-str.jpg)

> “Just as the name implies, this is an image of the estimated accumulation since the precipitation began. The accumulation continues until there is no precipitation for one hour anywhere within the range of the radar. Often, in prolonged rainy periods, this accumulation can exceed five days or more.
>
> As in the case of the one-hour precipitation image the radar does a great job at correcting itself, there are times when the radar will be out of calibration. If the radar is "hot" \(reporting echoes too strong\) then the rainfall estimates will be an overestimate. Conversely, a "cool" radar will underestimate the precipitation. Always check nearby radars to see if they are reporting similar information to what is viewed by your local radar.
>
> Also, hail makes an excellent reflector of energy. Thunderstorms with hail will overestimate the amount of precipitation and the larger the hailstones, the greater the overestimate.”
>
> -**National Weather Service** [**"Radar Images: Precipitation"**](https://www.weather.gov/jetstream/radarprecip)

## References and Additional Content

**National Weather Service JetStream -** [**Introduction to Doppler Radar**](https://forecast.weather.gov/jetstream/doppler/ridgeimages.htm#stp)

**GRLevelX -** [**User Manual**](http://www.grlevelx.com/manuals/grearth/radar.htm)

**Wunderground -** [**Understanding Radar**](https://www.wunderground.com/prepare/understanding-radar%20)

**Envirodata -** [**Gibson Radar 3 Explanation**](http://www.envirodata.org/files/gibson_radar_3_explanation.htm%20)

**WeatherObservatory.com -** [**"Weather Observatory"**](https://www.weatherobservatory.com/)

