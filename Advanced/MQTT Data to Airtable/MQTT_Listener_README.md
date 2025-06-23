# n8n MQTT Listener – Store Sensor Data in Airtable

This workflow subscribes to MQTT messages on the topic prefix `test/michael/` and stores incoming values in separate Airtable tables based on their topic. It is designed to work with data from an MQTT-based weather station or similar sensor setup.

## Features

- Subscribes to all topics under `test/michael/` using `test.mosquitto.org` as the MQTT broker.
- Supports temperature, humidity, and wind speed topics.
- Automatically stores values in different Airtable tables.
- Unknown topics are stored in a separate fallback table.

## Airtable Setup

Create a new Airtable base named **"N8N Test"** with the following tables:

### 1. Temperature Table

- **Table name:** `Temperature`
- **Fields:**
  - `id` (Single line text, primary field)
  - `Timestamp and Temperature` (Single line text)

### 2. Humidity Table

- **Table name:** `Humidity`
- **Fields:**
  - `id` (Single line text, primary field)
  - `Timestamp and Humidity` (Single line text)

### 3. WindSpeed Table

- **Table name:** `WindSpeed`
- **Fields:**
  - `id` (Single line text, primary field)
  - `Timestamp and WindSpeed` (Single line text)

### 4. Unknown Topic Table

- **Table name:** `MQTT Unknown`
- **Fields:**
  - `id` (Single line text, primary field)
  - `Topic` (Single line text)
  - `Message` (Single line text)

## How It Works

1. **MQTT Trigger**:  
   Subscribes to all topics under `test/michael/` using `test.mosquitto.org`. Messages are received in real time.

2. **Edit Fields**:  
   Adds a constant field `TOPIC_PREFIX = test/michael` to allow flexible topic matching. All other fields are preserved.

3. **Switch**:  
   Based on the topic, the message is routed to one of the following:
   - `Temperature Table`
   - `Humidity Table`
   - `WindSpeed Table`
   - `Unknown Topic Table` (fallback)

4. **Airtable Nodes**:  
   Each matched message is upserted (insert/update) into the appropriate table.

