# Google WiFi Home Assistant Integration

This integration provides control and monitoring of the Google WiFi system within Home Assistant.

### Platforms:

#### Binary Sensor:

The binary_sensor platform will show the access points that are configured in your system and their connection status to the Internet (on = connected). 

Additionally there is a custom service to allow you to reset either a single access point or the whole wifi system:

##### Service: googlewifi.reset

|Parameter|Description|Example|
|-|-|-|
|entity_id|Access point or system to restart.|binary_sensor.this_access_point|

#### Device Tracker:

The device_tracker platform will report the connected (home/away) status of all of the devices which are registered in your Google Wifi network. Note: Google Wifi retains device data for a long time so you should expect to see many duplicated devices which are not connected as part of this integration. There is no way to parse out what is current and what is old.

#### Switch:

The switch platform will allow you to turn on and off the internet to any connected device in your Google Wifi system. On = Internet On, Off = Internet Off / Paused. Additionally there are two custom services to allow you to set and clear device prioritization.

##### Service: googlewifi.prioritize

|Parameter|Description|Example|
|-|-|-|
|entity_id|The entity_id of the device you want to prioritize.|switch.my_iphone|
|duration|The duration in hours that you want to prioritize for.|4|

##### Service: googlewifi.prioritize_reset

|Parameter|Description|Example|
|-|-|-|
|entity_id|The entity_id of a device on the system you want to clear.|switch.my_iphone|

Note: Only one device can be prioritized at a time. If you set a second prioritization it will clear the first one first.

#### Light:

The light platform allows you to turn on and off and set the brightness of the lights on each of your Google Wifi hubs. (Just for fun).

## Install

To install this integration you will need a Google Refresh Token.

The only way that I have found to get a Refresh token is to go to: [Google Dev Console](https://console.cloud.google.com/project?pli=1) \
and create a new application, there are plenty of guides on how to do this. Then go to [Google Auth Playground](https://developers.google.com/oauthplayground/), go to settings and select use own creds, then authorize any api (I did Drive auth). There should be a button to exchage request for tokens or something, click that and get the token.

Once installed, restart Home Assistant and go to Configuration -> Integrations and click the + to add a new integration.

Search for Google WiFi and you will see the integration available.

Enter the refresh token, your email and a android id if you have on in the integration configuration screen and hit submit.

Enjoy!