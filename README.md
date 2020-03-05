# alice-mqtt-dynamic
Node-RED mqtt node reproduced from https://github.com/xTheRamon/node-red-contrib-mqtt-dynamictopic with thanks. 
Going to attempt to make changes allowing the Paho client to be configured for MQTT over WS. Cross your fingers.

# this version now supports websockets.
breaking change: the 'port' input in the configuration node is no longer available.
the 'host' name must be as:

```
<scheme>://<domain>:<port>
```

the string is submitted directly.

# node-red-contrib-mqtt-dynamictopic (from the original)
This is a node module for node-red that is identical to the default MQTT node. The difference with the MQTT node is that this dynamic node supports topics/channels passed through msg.topic.

# Installing
Simply install using the palette in node-red.

### Creds
I have used `node-red-contrib-mqtt-env` as a raw base for this node. Thank you.

# Version
This is a fork of `node-red-contrib-mqtt-dynamictopic`
=> correct multi subscriptions usage and unsubscriptions.


