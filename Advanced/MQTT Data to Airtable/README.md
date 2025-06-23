# n8n MQTT Sensor Data Project

This project demonstrates how to simulate and collect sensor data using two connected n8n workflows. One workflow acts as a weather station and publishes simulated data via MQTT. The other subscribes to these messages and stores the values in Airtable.

## Project Overview

This project consists of two parts:

### 1. MQTT Weather Station (Publisher)

This workflow simulates a weather station that generates and publishes random sensor values (temperature, humidity, wind speed) to a public MQTT broker (`test.mosquitto.org`) every 10 seconds.

- Topic format: `test/michael/{SensorType}`
- Each message includes a timestamp and the simulated value
- No authentication required

For more details, see: [`MQTT_Weather_station_README.md`](./MQTT_Weather_station_README.md)

### 2. MQTT Listener (Subscriber & Storage)

This workflow subscribes to all topics under `test/michael/` and processes the received messages. Based on the topic name, it routes the data to the corresponding Airtable table:

- `test/michael/Temperature` → stored in the **Temperature** table
- `test/michael/Humidity` → stored in the **Humidity** table
- `test/michael/WindSpeed` → stored in the **WindSpeed** table
- Any unknown topic → stored in a fallback table called **MQTT Unknown**

For more details, see: [`MQTT_Listener_README.md`](./MQTT_Listener_README.md)

## Notes

- Both workflows are designed to run independently but can be deployed together in a single n8n instance.
- The project uses the `test.mosquitto.org` broker, which is public and unsecured. Do not use it for sensitive or production data.
- The topic structure is flexible and defined via the `TOPIC_PREFIX` field.