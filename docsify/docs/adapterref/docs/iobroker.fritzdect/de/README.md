![Logo](media/fritzdect_logo.png)
# ioBroker.fritzdect

[![NPM version](http://img.shields.io/npm/v/iobroker.fritzdect.svg)](https://www.npmjs.com/package/iobroker.fritzdect)
[![Downloads](https://img.shields.io/npm/dm/iobroker.fritzdect.svg)](https://www.npmjs.com/package/iobroker.fritzdect)
[![Build Status](https://travis-ci.org/foxthefox/ioBroker.fritzdect.svg?branch=master)](https://travis-ci.org/foxthefox/ioBroker.fritzdect)

[![NPM](https://nodei.co/npm/iobroker.fritzdect.png?downloads=true)](https://nodei.co/npm/iobroker.fritzdect/)

Fritzbox DECT adapter for ioBroker

## Installation:
released version on npm with
```javascript
 npm install iobroker.fritzdect
```


or the actual version from github with 
```javascript
npm install https://github.com/foxthefox/ioBroker.fritzdect/tarball/master --production
```
## Setup

IP-address and password of Fritzbox should be defined in io-package.json or via admin page, before the first start of the instance.

The devices are detected automatically during startup of fritzdect instance.

the widget requires that also vis-metro and vis-jqui-mfd are installed

## ioBroker objects

objects in *italic* are not part of all fritz.box configurations

### all devices
|Object|Value|settable|Description|
|--------|-------|:-:|--------|
|devicetype.id|text|-|internal id of device|
|devicetype.name|text|-|name of device|
|devicetype.mode|text|-|mode, manuell or auto|
|devicetype.present|boolean|-|true/false -> connected/not available|
|devicetype.productname|text|-|product name|
|devicetype.manufacturer|text|-|product manufacturer|
|devicetype.fwversion|text|-|product FW version|

### groups
|Object|Value|settable|Description|
|--------|-------|:-:|--------|
|group.masterdeviceid|text|-|internal id of group|
|group.members|text|-|member id's of group|

### switch e.g DECT200/DECT210
|Object|Value|settable|Description|
|--------|-------|:-:|--------|
|DECT200.state|boolean|x|true/false -> ON/OFF|
|DECT200.power|value|-|actual power in W|
|DECT200.energy|value|-|actual energy consumption in Wh|
|DECT200.lock|boolean|-|UI/API lock|
|DECT200.devicelock|boolean|-|Button lock|
|*DECT200.temp*|value|-|actual temperature in °C|
|*DECT200.voltage*|value|-|actual voltage in V|

### thermostat eg. COMET/DECT300/ Heater group
|Object|Value|settable|Description|
|--------|-------|:-:|--------|
|COMET.temp|value|-|actual temperature in °C|
|COMET.targettemp|value|x|target temperature in °C|
|COMET.comfytemp|value|-|comfort temperature in °C|
|COMET.nighttemp|value|-|night temperature in °C|
|COMET.mode|array|x| 0=AUTO/1=OFF/2=ON state of thermostat|
|COMET.lasttarget|value|-| last target temperature in °C|
|COMET.batterylow|boolean|-|battery status|
|COMET.errorcode|number|-|errorcode|
|COMET.lock|boolean|-|UI/API lock|
|COMET.devicelock|boolean|-|Button lock|
|*COMET.battery*|value|-|actual capacity in %|
|*COMET.summeractive*|boolean|-|summer program status|
|*COMET.holidayactive*|boolean|-|holiday program status|

### repeater e.g. DECT100
|Object|Value|settable|Description|
|--------|-------|:-:|--------|
|DECT100.temp|value|-|actual temperature in °C|

### contact
|Object|Value|settable|Description|
|--------|-------|:-:|--------|
|Contact.state|boolean|-|true/false -> ON/OFF|

### guest WLAN
|Object|Value|settable|Description|
|--------|-------|:-:|--------|
|GuestWLAN.state|boolean|x|true/false -> ON/OFF|


## Known Issues:
After startup of adapter the firmware version of fritzbox is requested, some models do not respond to this request and therefore an error is logged.

## TODO:
* universal object names
* improvement of thermostat mode to text representation (auto, off, boost, comfort, night), comfort and night are also auto mode, but preset to the parametrized value
* widget for thermostat
* enhanced automated testing

## Changelog
### 0.1.2
* errorcode string->number
* batterylow -> boolean
* switch in admin for non native API call for battery charge in % (shall prevent 403 message logs)

### 0.1.1
* switch for GuestWLAN when no access is granted and polling creates an error
* check for devices in admin page for better access to the xml/json stream from fritzbox
* admin v3 implemented

### 0.1.0
* major code change to use the xml stream instead the dedicated API-commands for the dedicated values
* creation of objects according the feedback from fritzbox
* support of groups
* still usage of non-universal object names
* more objects

### 0.0.14
* correction of temp offset influence

### 0.0.13
* DECT200 voltage new object
* DECT200 mode/lock value polling
* Comet mode as number and not array
* ADMIN v3

### 0.0.12
* changed state to  mode AUTO/OFF/ON for thermostat (including datapoint lasttarget when going back to AUTO)
* added name state for thermostat
* DECT100 temperature reading
* Contact reading

### 0.0.11
* added state OFF/ON for thermostat

### 0.0.10
* change to object oriented interface
* getOSversion when starting for log

### 0.0.9
* values '1' accepted for ON
* values '0' accepted for OFF

### 0.0.8
* messages info-> debug
* values 1/true/on/ON accepted for ON
* values 0/false/off/OFF accepted for OFF

### 0.0.7
* current temp of Comet/DECT300
* cyclic polling GuestWLAN

### 0.0.6
* correction targettemp in DECT200 section

### 0.0.5
* setTemp on COMET
* GuestWlan corrected

### 0.0.4
* cyclic status polling

### 0.0.3
* user now configurable

### 0.0.2
* metro widget for Dect200
* smartfritz-promise->fritzapi
* running version, tested with 1x DECT200 and Fritzbox FW=6.51 on Win10 with 4.5.0 and raspberry 4.7.0

### 0.0.1
* running version, tested with 1x DECT200 and Fritzbox FW=6.30

## License

The MIT License (MIT)

Copyright (c) 2018 foxthefox <foxthefox@wysiwis.net>