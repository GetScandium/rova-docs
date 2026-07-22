# Scheduling

Automating your mobile tests is only half the battle; running them consistently is where you get the most value. **Rova Mobile's** scheduling system allows you to run your continuous mobile testing flows on a recurring basis without manual intervention.

### Creating a Schedule

To create a new automated run, navigate to the Schedules page and click Create Schedule to open the setup modal.

#### 1. Basic Information

* Schedule Name: Give your schedule a clear, identifiable name (e.g., `Nightly Regression Tests`).
* Description (Optional): Add a quick note to explain what this schedule covers or who should be notified.

#### 2. Choose Your Target (Execution Plan)

* Linked Plan: Select the specific Execution Plan you want to automate. Because Execution Plans group multiple testing goals into a single device session, this ensures your scheduled runs are highly efficient.

#### 3. When to Execute

Configure the exact frequency and timing for your automated device runs:

* **Frequency**: Choose how often the tests should repeat (e.g., Daily, Weekly, Hourly, or custom intervals).
* **Time**: Set the exact time of day you want the execution to kick off (e.g., `02:00`).
* **Timezone**: Select your preferred timezone (e.g., `UTC (UTC+0)`) to make sure tests run exactly when your team expects them, regardless of where your developers are located globally.

### Best Practices for Scheduling

#### 1. Run during "Off-Peak" Hours

Schedule large mobile regression plans to run overnight or when your development team is less active. This ensures that any fresh device failure logs or screen recordings are waiting for your mobile engineers first thing in the morning.

#### 2. Leverage Shared Context

Since schedules target Execution Plans, ensure your plans are optimized to utilize Shared Context. This avoids wasting execution time on repetitive actions like logging in or going through onboarding flows on the virtual device for every single goal.

#### 3. Hook Up Slack Alerts

Always configure Notifications (like your Slack integration) for your schedules. Automated testing is only useful if the right team members are instantly alerted the moment a build breaks on a virtual device.

#### 4. Watch for Overlapping Runs

Be mindful of how long your execution plan takes to complete versus its frequency. If a complex mobile flow takes 40 minutes to clear but is scheduled to run every 30 minutes, you might run into resource conflicts or exhaust your runtime credits unnecessarily.

### Monitoring Scheduled Runs

The Schedules tab in the dashboard provides a clear historical overview of all automated mobile runs. From here, you can quickly see:

* The next scheduled execution time based on your set timezone.
* The success or failure rate of the last 10 automated runs.
* A quick toggle switch to instantly pause or resume any active schedule.
