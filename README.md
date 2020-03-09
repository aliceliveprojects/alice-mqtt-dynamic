# alice-mqtt-dynamic
This is a Node-RED component which allows subscription to an MQTT topic specified by an input msg. It is a replacement for mqtt-dynamic.
Reproduced from https://github.com/xTheRamon/node-red-contrib-mqtt-dynamictopic with thanks. 

This component supports websockets ONLY.
The node is set-up by specifiying:

```
<scheme>://<domain>:<port>
```

Supported schemes are:

```
ws
wss (ws with TLS)
```


# Project
This node was developed for use in Alice LiveProjects: Pi Scalextric, https://github.com/aliceliveprojects/pi_scalextric
We needed to modify it to use websockets, rather than MQTT over TCP; the public MQTT broker we were using was not reliable enough, so we swapped to one we could deploy on Heroku: https://github.com/aliceliveprojects/alice-mqtt-broker.


# development and debugging

## set-up
We run this node locally to a Node-RED installation, on a Raspberry Pi: It is not installed via the Pallet Manager / npm.

1. Raspberry Pi: clean install of Raspbian Buster.
1. Set-up a development environment: debug remotely from a 'proper' PC / Mac via a router. See here: [here](https://github.com/aliceliveprojects/little_blue_pi/blob/master/documentation/worklogs/27.01.2020.md) 
1. Ensure Node RED can be run, and that there is a flow which utilises'https://github.com/xTheRamon/node-red-contrib-mqtt-dynamictopic', available from the pallete manager.
1. Use VSCode's git client to download this repo to the RPi.


## installation
To install the node:

1. see: https://nodered.org/docs/creating-nodes/first-node
1. on the RPi: bring up a terminal and use:  `cd ~/.node-red`
1. on the RPi: bring up the file manager: `pcmanfm .`  
1. use the filemanager to navigate to this repo, and copy the path to its directory we'll call it repo_path
1. in terminal, `npm install <repo_path>
1. This will install node-red-contrib-alice-mqtt-dynamic as a node in the Node-RED palette manager
1. The node will be substituted for any 'MQTT Dynamic` nodes in the flow.

## debugging
VSCode has a debugger, which can be configured to attach to a node process. Node-RED is built on node, and run as a Node process.
We set-up the VSCode running remotely on the RPi to debug the Node-RED process. 

1. Obtain the process id (PID) of the Node-RED process:
    1. On the RPi, bring up the task manager.
    1. In the task manager, search for processes named 'node'. There are a few.
    1. disconnect VSCode from the remote host. This will remove most node processes.
    1. stop the node red process: in a terminal on RPi: `node-red-stop`. This will remove any other node processes.
    1. kill any other node processes, using the task manager. (Dangerous, if you don't know who they belong to)
    1. restart node-RED: in a terminal on RPi: `node-red-start`
    1. in the RPi task manager note the PID of the new node process which is spawned.
1. Connect the VSCode debugger to the process:
    1. Connect VSCode to the RPi again (restart the remote connection)
    1. In this repo, find the /.vscode/launch.json file
    1. add the following, which sets up the VSCode debugger to attach to a process and replace PROCESS_ID with the id you noted.

    ```json
        {
            "type": "node",
            "request": "attach",
            "name": "AttachProcess",
            "processId": "PROCESS_ID"
        }
    ```    

here's an example of the full file:

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "skipFiles": [
                "<node_internals>/**"
            ],
            "program": "${workspaceFolder}/mqtt-dynamic.js"
        },
        {
            "type": "node",
            "request": "attach",
            "name": "AttachProcess",
            "processId": "PROCESS_ID"
        }
    ]
}
```

    1. Test, by placing a break-point in mqttConnectionPool.js


# node-red-contrib-mqtt-dynamictopic (from the original)
This is a node module for node-red that is identical to the default MQTT node. The difference with the MQTT node is that this dynamic node supports topics/channels passed through msg.topic.

# Installing
Simply install using the palette in node-red.

### Creds
I have used `node-red-contrib-mqtt-env` as a raw base for this node. Thank you.

# Version
This is a fork of `node-red-contrib-mqtt-dynamictopic`
=> correct multi subscriptions usage and unsubscriptions.


