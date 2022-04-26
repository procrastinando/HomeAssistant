# HomeAssistant
#### A compilation of the sensors in my home assistant using ESPhome

## 1. Temperature and Humidity sensor for the room
#### Using an AHT10 sensor on a D1 mini.

<p align="center"><img src="https://raw.githubusercontent.com/procrastinando/HomeAssistant/main/room.JPG" width="400"></p>

```i2c:
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

#### Using an DHT11 sensor and an ESP01, using a 0.75 lambda to calibrate the temperature.

<p align="center"><img src="https://raw.githubusercontent.com/procrastinando/HomeAssistant/main/room2.jpg" width="400"></p>

```sensor:
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
#### Using a DHT11 and MQ2 sensors on a D1 mini.

<p align="center"><img src="https://raw.githubusercontent.com/procrastinando/HomeAssistant/main/kitchen.JPG" width="400"></p>

```sensor:
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

## 3. RGB, LDR and motion sensor
#### A ESP8266 Witty Cloud has RGB and LDR integrated, while the motion sensor used is a HC-SR501.

<p align="center"><img src="https://raw.githubusercontent.com/procrastinando/HomeAssistant/main/light.jpg" width="400"></p>

```# RGB
light:
  - platform: rgb
    name: "Light sensor"
    red: output_component1
    green: output_component2
    blue: output_component3

output:
  - platform: esp8266_pwm
    id: output_component1
    pin: GPIO15

  - platform: esp8266_pwm
    id: output_component2
    pin: GPIO12
    
  - platform: esp8266_pwm
    id: output_component3
    pin: GPIO13
    
# LDR Light Sensor
sensor:
  - platform: adc
    pin: A0
    name: "LDR sensor"
    update_interval: 2s
    filters:
      - multiply: 3.3

# Motion sensor
binary_sensor:
  - platform: gpio
    pin: GPIO14
    name: "PIR sensor"
    device_class: motion
```

## 4. Moisture sensor for the plants
#### I still have one problem calibrating this sensor, besides, is not corrosion proof so I would not recommend it.

<p align="center"><img src="https://raw.githubusercontent.com/procrastinando/HomeAssistant/main/moisture.jpg" width="400"></p>

```sensor:
  - platform: adc
    pin: A0
    name: "Banana moisture Sensor"
    update_interval: 2s
    filters:
      - multiply: 100
    unit_of_measurement: "%"
    icon: "mdi:percent"
```
