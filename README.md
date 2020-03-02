# alice-mqtt-dynamic
Node-RED mqtt node reproduced from https://github.com/sajayantony/node-red-contrib-mqtt-dynamic with thanks. Going to attempt to make changes allowing the Paho client to be configured for MQTT over WS. Cross your fingers.


# MQTT Dynamic (from the original)

A fork of the [MQTT implemenation](https://github.com/node-red/node-red/blob/master/nodes/core/io/10-mqtt.js) that supports back pressure. The `Complete MQTT` node enables the trigger to continue recieving. If we complete as the next step then the this is almost equivalent to the concurrent model. 
