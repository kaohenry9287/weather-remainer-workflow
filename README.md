# Daily Weather Automation Workflow
<img width="1011" height="535" alt="workflow_screenshot" src="https://github.com/user-attachments/assets/035e6b6c-1458-4820-89cd-547d08903738" />

An n8n workflow that fetches daily weather data, generates AI-powered insights using Claude, and sends personalized weather emails with intelligent clothing recommendations.

## API Setup & Key Config

### 1. OpenWeatherMap API
- Sign up at https://openweathermap.org/api
- Copy your API key from the dashboard

### 2. Claude API (Anthropic)
- Go to https://console.anthropic.com/
- Create API key in the dashboard

### 3. Gmail App Password
- Enable 2FA on your Gmail account
- Generate app password at https://myaccount.google.com/apppasswords
- Copy the 16-character password

---

## Supabase Setup

1. Create project at https://supabase.com/
2. Create table `weather_logs` with these columns:
   - `id` (UUID, primary key)
   - `run_at` (timestamp)
   - `city` (text)
   - `temperature` (float)
   - `temperature_unit` (text)
   - `condition` (text)
   - `humidity` (int)
   - `wind_speed` (float)
   - `alert_type` (text)
   - `raw_response` (json)

3. Get credentials from Settings → API:
   - **Project URL:** Your Supabase URL
   - **Service Role Key:** Use this (not the anonymous key)

---

## Email Configuration

1. Enable 2FA on Gmail
2. Create App Password at https://myaccount.google.com/apppasswords
3. In n8n workflow, authenticate with Gmail using your app password
4. Update "Send a message" node's "To" field with your email address

---

## How to Import & Run the Workflow

### Step 1: Import Workflow
1. Open n8n dashboard
2. Click menu (⋮) → "Import from file"
3. Select `weather-workflow.json`

### Step 2: Add Credentials
For each node, click "Credential to connect with" → "Create New Credential":
- **HTTP Request node:** Add OpenWeatherMap API key
- **AI Agent node:** Add Claude API key
- **Create a row node:** Add Supabase URL + Service Role Key
- **Send a message node:** Authenticate with Gmail

### Step 3: Configure Workflow
- **Edit Fields node:** Change city from "London" to your desired city
- **Schedule Trigger node:** Set time (default: 9 AM)
- **Send a message node:** Update "To" field with your email

### Step 4: Test & Activate
1. Click "Execute Workflow" to test
2. Check your email for the weather report
3. Click "Activate" to run daily on schedule

---

## Workflow Features

- ✅ Daily scheduled execution
- ✅ Weather data from OpenWeatherMap
- ✅ AI-generated clothing recommendations (Claude)
- ✅ Automatic alert detection (Heat, Frost, Precipitation)
- ✅ Dynamic emoji mapping for conditions
- ✅ Color-coded alerts based on severity
- ✅ Data saved to Supabase
- ✅ Beautiful HTML emails

---
