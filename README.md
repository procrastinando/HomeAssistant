# HomeAssistant
A compilation of the sensors in my home assistant using ESPhome

## 1. Temperatura Humidity sensor for the room
<img width="400" src="https://raw.githubusercontent.com/procrastinando/HomeAssistant/main/room.JPG">

Using an AHT10 and a D1 mini:

```
i2c:
  id: bus_a
  sda: D2
  scl: D1
  scan: True
  frequency: 8khz

sensor:
  - platform: aht10
    i2c_id: bus_a
    address: 0x38
    update_interval: 30s
    temperature:
      name: "Room Temperature"
      accuracy_decimals: 1
    humidity:
      name: "Room Humidity"
```
