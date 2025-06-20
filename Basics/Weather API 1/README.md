# Weather Report via Open-Meteo API

This workflow demonstrates how to retrieve current weather data using the Open-Meteo API and prepare it for messaging or further automation.

## Overview

This workflow contains the following steps:

1. **Manual Trigger** – Used to manually start the workflow (useful for testing).
2. **Get Weather** – Sends an HTTP GET request to Open-Meteo with coordinates for Vienna.
3. **Format Message** – Creates a readable weather summary text.
4. **Next Step Placeholder** – You can extend this workflow to send the weather information via:
   - Email (SMTP / Gmail)
   - Telegram
   - Slack or Discord
   - Push notifications
   - Google Sheets or Notion for logging

## API Request

The Open-Meteo API does not require an API key.

Example URL used:

```
https://api.open-meteo.com/v1/forecast?latitude=48.208&longitude=16.373&current_weather=true
```

The API returns current weather conditions including temperature and windspeed.

## Example Output

From the `Format Message` node:

```
The current temperature in Vienna is 23.4°C with windspeed 12 km/h.
```

## Customization

- Replace the coordinates if you want data for another location.
- Add output nodes (like Send Email, Telegram, Slack) after the format step.
- Replace Manual Trigger with Schedule Trigger if you want daily updates.

## Notes

- This workflow is intended as a basis for learning HTTP APIs and message automation in n8n.
- You can chain this with other services like Google Sheets, databases, or chat bots.
- When using a production trigger, replace the Manual Trigger with Webhook or Cron.
