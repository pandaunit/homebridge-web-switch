<p align="center">
  <a href="https://github.com/homebridge/homebridge"><img src="https://raw.githubusercontent.com/homebridge/branding/master/logos/homebridge-color-round-stylized.png" height="140"></a>
</p>

<span align="center">

# homebridge-web-switch

[![npm](https://img.shields.io/npm/v/@rsporny/homebridge-web-switch.svg)](https://www.npmjs.com/package/@rsporny/homebridge-web-switch) [![npm](https://img.shields.io/npm/dt/@rsporny/homebridge-web-switch.svg)](https://www.npmjs.com/package/@rsporny/homebridge-web-switch)

</span>

## Original project and motivation
This project has been forked from [phenotypic](https://github.com/phenotypic/homebridge-web-switch). Motivation: added new field `switchOnValue` in which you can specify different number instead of default 1.
I need this to set special mode for my Thessla Green recuperator, e.g. airing, open window, which can have different values than 1. This way I can expose only one endpoint via MODBUS protocol and set everything in switch config.

## Description

This [homebridge](https://github.com/homebridge/homebridge) plugin exposes a web-based switch to Apple's [HomeKit](http://www.apple.com/ios/home/). Using simple HTTP requests, the plugin allows you to turn on/off the switch.

Find script samples for the switch controller in the _examples_ folder.

## Installation

1. Install [homebridge](https://github.com/homebridge/homebridge#installation)
2. Install this plugin: `npm install -g homebridge-web-switch`
3. Update your `config.json` file

## Configuration

```json
"accessories": [
     {
       "accessory": "WebSwitchCustomValue",
       "name": "Switch",
       "apiroute": "http://myurl.com"
     }
]
```

### Core
| Key | Description | Default |
| --- | --- | --- |
| `accessory` | Must be `WebSwitchCustomValue` | N/A |
| `name` | Name to appear in the Home app | N/A |
| `apiroute` | Root URL of your device | N/A |

### Additional options
| Key | Description | Default |
| --- | --- | --- |
| `pollInterval` | Time (in seconds) between device polls | `300` |
| `listener` | Whether to start a listener to get real-time changes from the device | `false` |
| `timeout` | Time (in milliseconds) until the accessory will be marked as _Not Responding_ if it is unreachable | `3000` |
| `port` | Port for your HTTP listener (if enabled) | `2000` |
| `http_method` | HTTP method used to communicate with the device | `GET` |
| `username` | Username if HTTP authentication is enabled | N/A |
| `password` | Password if HTTP authentication is enabled | N/A |
| `model` | Appears under the _Model_ field for the accessory | plugin |
| `serial` | Appears under the _Serial_ field for the accessory | apiroute |
| `manufacturer` | Appears under the _Manufacturer_ field for the accessory | author |
| `firmware` | Appears under the _Firmware_ field for the accessory | version |
| `switchOnValue` | Override default switch on value | `1` |

## API Interfacing

Your API should be able to:

1. Return JSON information when it receives `/status`:
```
{
    "currentState": INT_VALUE
}
```

2. Set the state when it receives:
```
/setState?value=INT_VALUE
```

### Optional (if listener is enabled)

1. Update `state` following a manual override by messaging the listen server:
```
/state?value=INT_VALUE
```
