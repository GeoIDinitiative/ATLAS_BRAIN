# PLAYBOOKS.md — distilled procedures

Written primarily by the TEACHER pass (the cloud model, when a key is set):
step-by-step procedures for workflows that recur, written so a small local
model can follow them instead of re-deriving them. Edit freely — this file is
yours, and it is injected into every turn for every backend.

## Managing Test Automations
When: A user (or you) creates a test automation to verify a tool or workflow (e.g., a "Test weather check" automation).
Steps:
1. Create the automation in the Automations tab with a name clearly prefixed "Test".
2. Trigger it once, manually or by its schedule, to confirm it works.
3. As soon as it has succeeded once, go to the Automations tab and DELETE it (or set it to disabled/no schedule).
4. Never leave a test automation on a recurring short interval (e.g., every 1 minute).
Verify: The Automations tab no longer lists the test automation, or it shows as disabled with no upcoming runs.
Avoid: Leaving a test automation running repeatedly. A "Test weather check" automation was left running every ~60-90 seconds for over an hour, filling the daily log with 50+ near-duplicate entries and wasting API calls.

## Diagnosing Automation ReadTimeout Failures
When: The daily log shows one or more entries like `[automation:<name>] Failed: ReadTimeout('')`.
Steps:
1. Treat a single ReadTimeout as transient (network/API hiccup), not a broken automation.
2. Look at the next few scheduled runs of the same automation in the daily log.
3. If a later run shows a normal successful result (e.g., a real temperature value), the issue resolved itself — take no action.
4. If ReadTimeout repeats for more than ~10 minutes across multiple runs with no success, suspect a real network or API outage. Check the device's internet connection.
5. If the failures persist beyond that, open the Automations tab and disable the automation until the underlying tool/API is confirmed working again.
Verify: Subsequent log entries for that automation show real data instead of "Failed: ReadTimeout".
Avoid: Panicking or reconfiguring the automation after just one ReadTimeout — wait for a few more scheduled runs first.

## Cleaning Up Runaway / Spammy Automations
When: The daily log contains many near-duplicate entries from the same automation fired repeatedly within a short window (e.g., every 60-90 seconds for an hour or more).
Steps:
1. Open the Automations tab.
2. Find the automation by its name (shown in the log line as `[automation:<name>]`).
3. Check its configured interval/schedule.
4. If the interval is too frequent for its purpose (e.g., a weather check running every minute instead of hourly/daily), either edit the schedule to a sensible interval or delete the automation entirely if it was only for testing.
5. Save the change.
Verify: No new log entries appear from that automation right after cleanup, and later entries (if any) appear at the newly intended interval, not every ~1 minute.
Avoid: Ignoring log spam from a single automation — it makes it hard to find genuinely important log entries and wastes automation-run budget.