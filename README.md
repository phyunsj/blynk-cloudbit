

## [CLOUDBIT™](https://littlebits.com/cloudstart/) 

**Disclaimer:** All images are from [littleBits](https://shop.littlebits.com/products/cloudbit)

"The cloudBit is the easiest way to create internet­-connected devices. You can now snap the internet to anything! Retrofit your thermostat to control it remotely, or set up a sound-triggered alarm system that texts you alerts - the possibilities are endless." ..._from [littleBits](https://littlebits.com/)_

<p align="center">
<img src="https://github.com/phyunsj/blynk-cloudbit/blob/master/images/cloudbit.png" width="400px"/>
</p>
 
#### [Cloud API](http://developers.littlebitscloud.cc/) to access litteBits Cloud API endpoints to manage your cloudbits 
The littleBits Cloud API is rate limited to prevent abuse that would degrade our ability to maintain consistent API performance for all users. (host : `https://api-http.littlebitscloud.cc`)


## Blynk + Node-RED

<p align="center">
<img src="https://github.com/phyunsj/blynk-cloudbit/blob/master/images/blynk_nodered_littlebits.png" width="400px"/>
</p>

- "**Blynk** is a Platform with iOS and Android apps to control Arduino, Raspberry Pi and the likes over the Internet." ..._from [blynk.cc](https://www.blynk.cc/)_

- "**Node-RED** : a programming tool for wiring together hardware devices, APIs and online services in new and interesting ways. It provides a browser-based editor that makes it easy to wire together flows using the wide range of nodes in the palette that can be deployed to its runtime in a single-click." ..._from [nodered.org](https://nodered.org/)_

- [blynk + Node-RED](https://github.com/phyunsj/blynk-node-red) for the additional information.
- [littlebits-cloud-http](https://www.npmjs.com/package/littlebits-cloud-http) lightweight wrapper for littleBits Cloud HTTP API


## CLOUDBIT™ acts as an input

<p align="center">
<img src="https://github.com/phyunsj/blynk-cloudbit/blob/master/images/circuit-output.png" width="400px"/>
</p>

In a `function` node (triggered by [Blynk-ws](https://www.npmjs.com/package/node-red-contrib-blynk-ws) `read event` node),

```
// "access_token" and "device_id" are acquired from littlebit cloudcontrol setting page
var api = require('littlebits-cloud-http')
          .defaults({ access_token: '*****************' }); 

api.output({device_id: '****', percent: 50, duration_ms: 5000 }); 
```

<p align="center">
<img src="https://github.com/phyunsj/blynk-cloudbit/blob/master/images/blynk-cloudbit-output.png" width="400px"/>
</p>

## CLOUDBIT™ acts as an output

<p align="center">
<img src="https://github.com/phyunsj/blynk-cloudbit/blob/master/images/circuit-sub-pub.png" width="400px"/>
</p>

Create a new subscription for `device_id`. 

```
// "access_token" and "device_id" are acquired from littlebit cloudcontrol setting page
var api = require('littlebits-cloud-http')
          .defaults({ access_token: '*****************' }); 
api.subscribe( {
  subscriber_id : 'https://************',
  publisher_id  : 'device_id',
  publisher_events : [ 'amplitude' ]
});         
```

 **NOTE** [Cloud Control](http://control.littlebitscloud.cc/) and [littlebits Invent App](https://itunes.apple.com/us/app/littlebits-invent/id1021974711?mt=8) worked as advertised. However, the sub/pub model doesn't ( `littlebits/cloud-client-api-http` has no updates over 3 years.) I didn't find any suitable working example yet. `subscriber_id` was assgined with the public URL (Node on [Heroku](https://www.heroku.com) Platform) but no request was received. 
 
## Related Posts
- [Getting Started with CloudBit](http://discuss.littlebits.cc/t/getting-started-with-the-cloudbit/22483)
- [Exploring IoT Concepts with a CloudBit](https://www.designnews.com/electronics-test/exploring-iot-concepts-cloudbit/21164096047247)
- [LittleBits Now Lets You Build Your Own DIY Smart Home](https://gizmodo.com/littlebits-now-lets-you-to-build-your-own-diy-smart-hom-1609215918)
- [Cloud Weather Dashboard](https://github.com/littlebits/project-cloud-weather-dashboard)
