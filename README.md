# HomeAssistant
A compilation of the sensors in my home assistant using ESPhome

## 1. Temperature and Humidity sensor for the room

<img width="400" src="https://raw.githubusercontent.com/procrastinando/HomeAssistant/main/room.JPG">

Using an AHT10 sensor on a D1 mini:

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

<img width="400" src="https://raw.githubusercontent.com/procrastinando/HomeAssistant/main/room2.jpg">

Using an DHT11 sensor and an ESP01, using a 0.75 lambda to calibrate the temperature:

```
sensor:
  - platform: dht
    pin: GPIO2
    model: DHT11
    update_interval: 30s
    temperature:
      name: "Bedroom-2 Temperature"
      accuracy_decimals: 1
      filters:
      - lambda: return x * 0.75;
    humidity:
      name: "Bedroom-2 Humidity"
```

## 2. Temperature, Humidity and Smoke sensor for the kitchen
<img width="400" src="https://raw.githubusercontent.com/procrastinando/HomeAssistant/main/kitchen.JPG">

Using a DHT11 and MQ2 sensors on a D1 mini

```
sensor:
  - platform: dht
    pin: D1
    update_interval: 30s
    model: AUTO_DETECT
    temperature:
      name: "Kitchen Temperature"
      accuracy_decimals: 1
    humidity:
      name: "Kitchen Humidity"

  - platform: adc
    pin: A0
    name: "Kitchen Gas Sensor"
    update_interval: 30s
    filters:
      - multiply: 100
    unit_of_measurement: "%"
    icon: "mdi:percent"
```

## 3. 
