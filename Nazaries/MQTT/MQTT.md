# MQTT

## Essentials
- publish/subscribe messaging transport protocol.
- MQTT is build on top of TCP
- It is binary based, bidirectional and data-agnostic.
- Decople by elements, time and syncronization.

>Structure: \
>IP &rarr; TCP &rarr; MQTT

- Security Transport Level (TSL)
- Constructed based on Single Point of Failure(SPOF). Important to do a cluster broker.
- Broker in the hearth of MQTT

### Main Components:
#### Client
#### Broker

### Steps for connections:
1. TCP connection
2. MQTT connection 
3. MQTT connack

### Types of msgs:
1. Publish
2. Subscribe
3. Qos 

### Queued msg vs. retained msgs

### Last will statemnet

### Client Takeover






