# Scheduling Tests & Suites

Automating your tests is only half the battle; running them consistently is where you get the most value. Rova's scheduling system allows you to run tests on a recurring basis without manual intervention.

## Creating a Schedule

### 1. Choose Your Target
You can schedule an individual **Test** or an entire **Suite** (recommended).

### 2. Define the Frequency
Rova supports flexible scheduling options:
- **Interval-based**: Run every X hours or minutes.
- **Daily**: Run at a specific time every day.
- **Weekly**: Run on specific days of the week (e.g., Every Monday and Wednesday at 2 AM).
- **CRON Expression**: For advanced users, you can provide a standard CRON string for maximum control.

### 3. Select the Environment
Your scheduled tests will run on:
- **Rova Cloud**: Our managed infrastructure (default).

## Best Practices for Scheduling

### 1. Run during "Off-Peak" Hours
Schedule large regression suites to run when your development team is less active. This ensures that any failures are waiting in your inbox first thing in the morning.

### 2. Use "Continuity" for Scheduled Suites
If your scheduled suite involves complex setups, ensure **Continuity Mode** is enabled so that tests can share state and run more reliably.

### 3. Notifications
Always configure **Notifications** (Email, Slack, or Webhook) for your schedules. There's no point in running tests if nobody is alerted when they fail.

### 4. Overlapping Schedules
Be mindful of overlapping schedules. If a suite takes 30 minutes to run but is scheduled every 15 minutes, you may run into resource constraints or credit exhaustion.

## Monitoring Scheduled Runs
The **Schedules** tab in the dashboard provides a calendar view and history of all automated runs. You can see:
- Next scheduled execution time.
- Success/Failure rate of the last 10 runs.
- Quick toggle to pause or resume any schedule.
