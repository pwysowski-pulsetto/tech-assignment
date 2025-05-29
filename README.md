
# 🛠 Technical Task: Daily Push Notification Service (.NET 8, OneSignal)

## 🧾 Overview

Build a **.NET 8 Web API** that sends a **daily push notification** to users via **OneSignal**, based on each user's preferred time of day. Users must explicitly enable notifications and set a preferred time before messages are scheduled.

---

## ✅ Functional Requirements

### 1. MySQL Table: `users`

| Field                   | Type                        | Description                          |
|------------------------|-----------------------------|--------------------------------------|
| `user_id`              | string (PK)                 | Unique user identifier               |
| `platform`             | enum(`ios`, `android`)      | Mobile platform                      |
| `notifications_enabled`| boolean                     | Whether the user allows notifications|
| `notification_time`    | TIME (nullable)             | Time of day (UTC) to send message    |

---

### 2. API Endpoints

#### `POST /api/notifications/setNotificationTime`
Sets the time of day the user wants to receive daily notifications.

**Request Body:**
```json
{
  "userId": "string",
  "timeUtc": "HH:mm"
}
```

#### `POST /api/notifications/enableNotifications`
Marks the user as subscribed to push notifications.

**Request Body:**
```json
{
  "userId": "string"
}
```

#### `POST /api/notifications/disableNotifications`
Disables notifications for the user.

**Request Body:**
```json
{
  "userId": "string"
}
```

---

### 3. Notification Logic (Cron Job)

- A **background job** runs every minute and:
  - Finds users where:
    - `notifications_enabled = true`
    - `notification_time IS NOT NULL`
    - Current UTC time matches `notification_time` (within a 1-minute window)
  - Sends a push message via **OneSignal**
  - Logs the notification result
  
---

## 📦 Deliverables

Your GitHub repository should include:

- ✅ .NET 8 Web API code
- ✅ Dockerfile and `docker-compose.yml`
- ✅ MySQL schema and seed SQL (if needed)
- ✅ A `README.md` with:
  - Setup instructions
  - OneSignal config steps
  - Sample requests for the 3 endpoints

---

## ⚙️ Tech Stack

- .NET 8 Web API
- EF Core 8
- MySQL 8
- OneSignal REST API
- Docker + Docker Compose
- BackgroundService for cron-like scheduling

---

## 🧠 Bonus Points

- Prevent duplicate sends within the same day
- Add unit tests for time-matching logic
- Support multiple time zones

---

## 🔐 OneSignal Setup (Required)

This task uses [OneSignal](https://onesignal.com), which is **free to use**.

You must:
- Create a free OneSignal account
- Set up an app for push notifications
- Use your own OneSignal **App ID** and **REST API Key** in your `.env` or `appsettings.json`
- **Do not hardcode keys in source code**
- Share your App ID and API key with us privately so we can test your implementation

---

## ✅ Summary of Expectations

- Notification scheduling based on user preference
- OneSignal integration (real or mocked)
- MySQL-backed data storage
- Clean, testable code

---

## ▶️ How to Submit

1. Fork this repository or create a new public repo
2. Implement the solution
3. Include a `README.md` with setup and sample requests
4. Submit your GitHub repo link

Good luck! 🚀

