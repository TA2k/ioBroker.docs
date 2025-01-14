![Logo](admin/zwave2.svg)

# ioBroker.zwave2

[![node](https://img.shields.io/node/v/iobroker.zwave2.svg)
![npm](https://img.shields.io/npm/v/iobroker.zwave2.svg)](https://www.npmjs.com/package/iobroker.zwave2)
[![changelog](https://img.shields.io/badge/read-Changelog-informational)](CHANGELOG.md)

![Number of Installations](http://iobroker.live/badges/zwave2-installed.svg)
![Number of Installations](http://iobroker.live/badges/zwave2-stable.svg)

![Test and Release](https://github.com/AlCalzone/iobroker.zwave2/workflows/Test%20and%20Release/badge.svg)
[![Language grade: JavaScript](https://img.shields.io/lgtm/grade/javascript/g/AlCalzone/ioBroker.zwave2.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/AlCalzone/ioBroker.zwave2/context:javascript)
[![Translation status](https://weblate.iobroker.net/widgets/adapters/-/zwave2/svg-badge.svg)](https://weblate.iobroker.net/engage/adapters/?utm_source=widget)

<h2 align="center">Z-Wave for ioBroker. But better.</h3>

Z-Wave 2 is a brand new Z-Wave implementation for ioBroker. It is based on [`zwave-js`](https://github.com/AlCalzone/node-zwave-js), which was written from the ground up for your benefit.

Unless [`ioBroker.zwave`](https://github.com/ioBroker/ioBroker.zwave/) it does not require `OpenZWave`. This means that the installation and updates are fast, and no compilation of static libraries and other complicated steps are necessary.

Furthermore, some devices just don't work in the original adapter, e.g. the Fibaro Roller Shutter 3.

Easy usage in ioBroker was kept in mind during the whole development. For example, some devices reuse configuration parameters to configure many different things. In this adapter, most of them are split into separate states and no complicated math is necessary:
| Config params in ioBroker.zwave2 | vs | Config params in ioBroker.zwave |
| --- | --- | --- |
| ![](docs/de/images/config-params.png) | vs | ![](docs/de/images/config-params-legacy.png) |

---

## Documentation and usage
* [FAQ](docs/en/FAQ.md)
* [Troubleshooting](docs/en/troubleshooting.md) · [bei Problemen](docs/de/bei-problemen.md)

---

## Changelog
[Older changes](CHANGELOG_OLD.md)
<!--
	Placeholder for next versions:
	### __WORK IN PROGRESS__
-->
### 2.0.0-alpha.0 (2021-09-17)
Upgraded to `zwave-js` version `8.3.2`. Notable changes include:
* **BREAKING:** Node.js `v12.22.2` is now the minimum
* **BREAKING:** User codes are no longer queried during the interview. They need to be queried manually on demand (not implemented yet).
* **BREAKING:** Reworked how endpoints and lifeline associations are handled. This solves reporting issues with many devices, but after a re-interview state IDs may change and some previously working devices may no longer report correctly. Please create an issue for every device that is affected by this.
* The device management was moved from the adapter settings to an extra `Z-Wave` tab.
* Some config parameters now correctly offer `0/1` as options instead of `0/-1`
* Fixed a bug where the cache file could be corrupted during a shutdown
* Support for Security S2
* Support for devices which use `Supervision CC` to send commands
* Support for factory resetting the controller
* Support for changing the region/frequency of the controller
* Support for replacing failed nodes while keeping the ID
* Some fixes for firmware updates

### 1.10.4 (2021-08-07)
* Fixed a bug where the daily config update check would cause a lot of internet traffic for an hour

### 1.10.3 (2021-07-14)
Upgraded to `zwave-js` version `7.12.0`. Notable changes include:
* Further improved handling of the legacy `alarmType` and `alarmLevel` values under some circumstances
* Improved support for Aeotec firmware updaters
* Nodes are no longer sent to sleep while a value change is planned to be verified
* Hardened the checks to prevent simultaneous write-accesses for the cache files
* The adapter should now be restarted when the serial connection is disconnected
* Fixed a bug where associatiations on endpoints had incorrect labels
* Updated dependencies
* Tons of new and improved config files

### 1.10.2 (2021-06-10)
Upgraded to `zwave-js` version `7.7.3`. Notable changes include:
* Improved how dropped invalid messages are logged in the Z-Wave logfile
* Improved handling of the legacy `alarmType` and `alarmLevel` values under some circumstances
* Improved handling of notification values for devices that support `Notification CC` version 2
* Improved how some devices with incorrect capability reports are queried
* Endpoints of multi channel devices should now always be queried with the correct CC version
* Throttled some automatic queries
* Avoid a situation where multiple instances of the adapter try to access the same cache files, potentially corrupting them
* Improved behavior of secure communication when transmission failures are involved
* Several new and improved config files

### 1.10.1 (2021-05-24)
Removed some warnings about wrong state value types in JS-Controller 3.3
Upgraded to `zwave-js` version `7.5.1`. Notable changes include:
* Improved stability
* Improved healing strategy
* Several config file changes

## License

MIT License

Copyright (c) 2019-2021 AlCalzone

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