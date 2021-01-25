![Logo](admin/tvprogram.png)
# ioBroker.tvprogram

[![NPM version](http://img.shields.io/npm/v/iobroker.tvprogram.svg)](https://www.npmjs.com/package/iobroker.tvprogram)
[![Downloads](https://img.shields.io/npm/dm/iobroker.tvprogram.svg)](https://www.npmjs.com/package/iobroker.tvprogram)
![Number of Installations (latest)](http://iobroker.live/badges/tvprogram-installed.svg)
![Number of Installations (stable)](http://iobroker.live/badges/tvprogram-stable.svg)
[![Dependency Status](https://img.shields.io/david/oweitman/iobroker.tvprogram.svg)](https://david-dm.org/oweitman/iobroker.tvprogram)
[![Known Vulnerabilities](https://snyk.io/test/github/oweitman/ioBroker.tvprogram/badge.svg)](https://snyk.io/test/github/oweitman/ioBroker.tvprogram)

[![NPM](https://nodei.co/npm/iobroker.tvprogram.png?downloads=true)](https://nodei.co/npm/iobroker.tvprogram/)

**Tests:** [![Travis-CI](http://img.shields.io/travis/oweitman/ioBroker.tvprogram/master.svg)](https://travis-ci.org/oweitman/ioBroker.tvprogram)

## tvprogram adapter for ioBroker

This adapter polls information about the television program at regular intervals. 
The data can be displayed in various widgets. 

The adapter is still in an alpha phase in which widgets / functions are still being tested, 
functions / widgets can be added and removed or completely exchanged.

References to issues or feature requests can be left or 
discussed in the iobroker forum in the corresponding thread

## Developer manual
The adapter can currently only be installed via github. This can be done in the iobroker in the "adapter" tab, 
with the expert view via the github button (cat symbol).

Then enter the url of the github repository https://github.com/oweitman/iobroker.tvprogram in the "any" tab and install it.

### Adapter Configuration

No configuration currently required

### Widgets

#### Time
This widget shows the current TV program on a timeline by TV channel.

To set it up, the adapter must have already accessed and filled the necessary data. 
Due to its size, the data is not stored in data points but in files and in the adapter's memory.
In the configuration, the widget only needs to be filled with any data point of the adapter (e.g.config).
The widget searches for all remaining data points automatically.

If the text behind the channel logos shows through, a background color must be selected in the widget.
it is generally a good approach to choose an explicit foreground and background color for the view or at least for the widget.
The Marker position ist updated every 15 seconds.

If something goes wrong after installation and the widget isnt diplayed correctly, please try the following command from shell:

iobroker upload all

The following attributes are available for configuration in vis

| Attribute             | Example            | Description                                           |
| --------------------- | ------------------ | ----------------------------------------------------- |
| tvprogram_oid         | tvprogram.0.config | A Datapoint of a instance of the tvprogram adapter.   |
| widthItem             | 120                | Standard width in pixels for a 30 minute segment      |
| heightRow             | 35                 | Height for each displayed line                        |
| headerfontpercent     | 125                | Character size in percent for the heading (time)      |
| broadcastfontpercent  | 75                 | Character size in percent for the broadcasts          |
| highlightcolor        | yellow             | color for the favorites                               |
| markerpositionpercent | 25                 | Position of the Marker in percent ot the widget width |
| dialogwidthpercent    | 90                 | size of the dialogs in percent of the widget          |
| dialogheightpercent   | 90                 | size of the dialogs in percent of the widget          |

#### Favorites
This widget shows a list of the selected favorites, sorted by date and time.

The following attributes are available for configuration in vis

| Attribute      | Example            | Description                                         |
| -------------- | ------------------ | --------------------------------------------------- |
| oid            | tvprogram.0.config | A Datapoint of a instance of the tvprogram adapter. |
| channelname    | no                 | Show logo (off) or channelname                      |
| showweekday    | yes                | Show Weekday                                        |
| maxfavorites   | 10                 | Max favorites to show                               |
| highlightcolor | yellow             | color for the favorites                             |

### Provided Datapoints

**config**
this datapoint contains the configuration of the widget information e.g. selected channels, selected favorites, etc.

**cmd**
this datapoint is used for internal communication between the widgets and the adapter

**selectchannel*
This datapoint is used to recognize a channel switch command with a click on the channel logo or the switch icon in the detail view.

**record**
This datapoint is set if the user clicks the record button in the detail view of a broadcast.
The provided data are

| field     | Example                    | Description            |
| --------- | -------------------------- | ---------------------- |
| startTime | 2021-01-01T00:10:00+01:00  | Start time             |
| endTime   | 2021-01-01T00:10:30+01:00  | End time               |
| title     | Title of the broadcast     | title of the broadcast |
| channel   | 7                          | Unique channel number  |
| channelid | zdf                        | Unique channel id      |

Functions:

- show tv data on timeline by tv channel
- show details about a tv broadcast if available
- show a marker of actual position with automatic scrolling
- configure displayed tv channels and order, reordering ist possible via dragNdrop.
- switch command via datapoint after click on logo
- zoomin/zoomout
- navigation next and prev days
- play button to switchchannel datapoint
- center zoom in next days
- return to today
- reset zoom
- favorite broadcasts
- copy text from Detailview
- markerposition is configurable
- dialog width and height is configurable 
- Datenpunkt record, der nach druck auf Knopf mit Aufnahmedaten gefüllt wird

### Todo

widget tvprogram: 
- widget for next Favorites
- broadcast reminders (Favorites widget?)
- to be discussed: dont want to see, broadcasts should be hidden
- to be discussed: Datenpunkt, mit allen Aufnahmedaten
- Problem: endless scroll in firefox
- Ideas for further widgets based on the existing TV program script
- Data adapter for other sources (Internet, hardware such as Enigma, VU-Box)
- ~~responsive design for detail view->no responsive design possible for jquery dialog, found another solution with fixed layouts for height>width~~
- ~~Problem: small Pixel glitch if scroll pane is completle on the left side~~

## Changelog

### 0.0.1
* (oweitman) initial release

## License
MIT License

Copyright (c) 2020 oweitman <oweitman@gmx.de>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.