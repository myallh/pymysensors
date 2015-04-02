# pymysensors
Python API for talking to a MySensors gateway

# Usage
Currently the API is best used by implementing a callback handler
```python
import pymysensors.mysensors as mysensors

def event(type, nid):
    print(type+" "+str(nid))

gw = mysensors.SerialGateway('/dev/ttyACM0', event)
gw.listen()
```

In the above example PyMysensors will call "event" whenever a node in the Mysensors network has been updated.

The data structure of a gateway and it's network is described below.
```
SerialGateway
    sensors - a dict containing all nodes for the gateway; node is of type Sensor

Sensor - a sensor node
    children - a dict containing all child sensors for the gateway
    id - node id on the MySensors network
    type
    sketch_name
    sketch_version
    battery_level

ChildSensor - a child sensor
    id - Child id on the parent node
    type - Data type, S_HUM, S_TEMP etc.
    value - the value
```

Getting the type and value of node 23, child sensor 4 would be performed as follows:
```
type = gw.sensors[23].children[4].type
value = gw.sensors[23].children[4].value
```