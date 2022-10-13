# Workshop 3.1

## Problem Statement

Commuters are feeling unsafe on both the vehicle and platform. Convince TfNSW to invest in a sensor solution.

## Sensors

- RFID sensors on platform and tram.

## Sensor Pseudocode

```
fire_train_guard()
if at_same_distance(sensor_train(), sensor_platform()) and train_stopped()
    open_doors()
```
