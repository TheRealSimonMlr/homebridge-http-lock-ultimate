# homebridge-http-lock-ultimate

[![npm](https://img.shields.io/npm/v/homebridge-http-lock-ultimate.svg)](https://www.npmjs.com/package/homebridge-http-lock-ultimate) [![npm](https://img.shields.io/npm/dt/homebridge-http-lock-ultimate.svg)](https://www.npmjs.com/package/homebridge-http-lock-ultimate)

## Description

This [homebridge](https://github.com/nfarina/homebridge) plugin exposes a web-based locking device to Apple's [HomeKit](http://www.apple.com/ios/home/). Using simple HTTP requests with post, body and header support, the plugin allows you to lock/unlock the device, i.e. Shelly 1 devices.

## Installation

1. Install [homebridge](https://github.com/nfarina/homebridge#installation-details)
2. Install this plugin: `npm install -g homebridge-http-lock-ultimate`
3. Update your `config.json` file

## Configuration examples
Configuration example for a Shelly 1 device controlled via Get Requests in local network. Resets it's state to locked automatically after 5 Seconds

```json
"accessories": [
     {
      "accessory": "HTTPLockUltimate",
      "name": "Front Door",
      "resetLock": "true",
      "resetLockTime": "5",
      "http_method": "GET",
      "openURL": "http://192.168.X.XX/relay/0?turn=on",
      "closeURL": "http://192.168.X.XX/relay/0?turn=off"
      }
]
```

This is a configuration example for a Shelly 1 device controlled via Post Requests to Shelly Cloud. Get's locked automatically after 5 Seconds.

```json
"accessories": [
     {
      "accessory": "HTTPLockUltimate",
      "name": "Front Door",
      "autoLock": "true",
      "autoLockDelay": "5",
      "http_method": "POST",
      "openURL": "https:/your.server.address/device/relay/control/",
      "openHeader": {
          "Content-Type": "application/x-www-form-urlencoded"
      },
      "openBody": "turn=on&channel=0&id=XXXXXXX&auth_key=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
      "closeURL": "https://your.server.address/device/relay/control/",
      "closeHeader": {
          "Content-Type": "application/x-www-form-urlencoded"
      },
      "closeBody": "turn=off&channel=0&id=XXXXXXX&auth_key=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
      }
]
```

### Core
| Key | Description | Default |
| --- | --- | --- |
| `accessory` | Must be `HTTPLockUltimate` | N/A |
| `name` | Name to appear in the Home app | N/A |
| `openURL` | URL to trigger unlock | N/A |
| `closeURL` | URL to trigger lock | N/A |

### Optional fields
| Key | Description | Default |
| --- | --- | --- |
| `autoLock` _(optional)_ | Whether your lock should re-lock after being opened (closeURL Request gets triggered) | `false` |
| `autoLockDelay` _(optional)_ | Time (in seconds) until your lock will auto lock if enabled | `5` |
| `resetLock` _(optional)_ | If your lock is locking itself after opened, use this option to reset the state automatically (Will not call closeURL and is ignored when using autoLock) | `false` |
| `resetLockTime` _(optional)_ | Time (in seconds) until your lock will be set to locked | `5` |

### Additional options
| Key | Description | Default |
| --- | --- | --- |
| `timeout` _(optional)_ | Time (in seconds) until the accessory will be marked as _Not Responding_ if it is unreachable | `5` |
| `http_method` _(optional)_ | HTTP method used to communicate with the device | `GET` |
| `openHeader` | Request Header to send in unlock request | N/A |
| `openBody` | JSON Body to send on open | N/A |
| `closeHeader` | Request Header to send in lock request | N/A |
| `closeBody` | JSON Body to send on close | N/A |
| `username` _(optional)_ | Username if HTTP authentication is enabled | N/A |
| `password` _(optional)_ | Password if HTTP authentication is enabled | N/A |
| `model` _(optional)_ | Appears under the _Model_ field for the accessory | plugin |
| `serial` _(optional)_ | Appears under the _Serial_ field for the accessory | version |
| `manufacturer` _(optional)_ | Appears under the _Manufacturer_ field for the accessory | author |
| `firmware` _(optional)_ | Appears under the _Firmware_ field for the accessory | version |
