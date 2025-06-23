# MQTT Weather Station (MQTT_Weather_station)

This n8n workflow simulates a simple weather station that publishes dummy sensor data (temperature, humidity, and wind speed) to an MQTT broker every 10 seconds.

## Features

- Simulates random weather values using a Code node
- Publishes the values to a public MQTT broker (`test.mosquitto.org`)
- Topics are prefixed via a central constant (`TOPIC_PREFIX`)
- Timestamp is included in each message
- Fully functional without any authentication (public broker)

## How it works

1. A `Schedule Trigger` starts the workflow every 10 seconds.
2. A `Set` node adds the constant `TOPIC_PREFIX` and passes along the timestamp.
3. A `Code` node generates random weather values and returns a single object with:
   - `Temperature` (20–29 °C)
   - `Humidity` (20–49 %)
   - `WindSpeed` (0–49 km/h)
4. The result is routed to three MQTT publish nodes:
   - Temperature → `TOPIC_PREFIX/Temperature`
   - Humidity → `TOPIC_PREFIX/Humidity`
   - Wind speed → `TOPIC_PREFIX/WindSpeed`
5. Each message includes a timestamp and the respective sensor value.

## Configuration

### MQTT Broker

This example uses:
- Host: `test.mosquitto.org`
- Port: `1883`
- No authentication required


