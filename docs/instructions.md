# Setup Instructions

## ✅ 1. Open Power Automate

Go to: https://make.powerautomate.com

Make sure you're signed in with your Microsoft 365 account.

## ✅ 2. Go to "Create"

On the left navigation menu:

**Create → Automated cloud flow**

You'll see this option along with others like Instant flow, Scheduled flow, Desktop flow, etc.

## ✅ 3. Name Your Flow

Enter a name for your flow, such as: **"Automatically decline on my OOO day"**

Then select the trigger type.

## ✅ 4. Set Up the Trigger

Choose: **"When an event is created (V3)"**

- This is the Office 365 Outlook connector
- It will listen for new calendar events
- The flow will process each event individually

## ✅ 5. Add a Condition

Click **"+ New step"** → **"Add an action"** → Search for **"Condition"**

Set the condition:
- **Left field:** Select "Organizer Email" from the dynamic content
- **Operator:** "is not equal to"
- **Right field:** Enter your own email address

This ensures the flow only acts on events **you didn't organize**.

## ✅ 6. Add "Respond to Event" (Yes Branch)

In the **"Yes"** branch, click **"+ Add an action"**

Search for and select: **"Respond to event"** (Office 365 Outlook)

Configure:
- **Event ID:** Select from dynamic content
- **Response:** Choose **"Decline"**
- **Comment:** Add a polite message explaining your absence:
  ```
  Hello,
  I'll be out of the office on this date for a compensatory day off. 
  This meeting has been automatically declined.
  
  Thank you for your understanding.
  ```
- **Send Response:** Toggle **ON**

## ✅ 7. Add "Delete Event" in Parallel (Optional)

In the **"Yes"** branch, next to the "Respond to event" action, click the **"+"** icon and select **"Add a parallel branch"**

Search for: **"Delete event"** (Office 365 Outlook)

Configure:
- **Calendar ID:** Select your calendar
- **Event ID:** Select from dynamic content (use the trigger output)

This will remove the declined event from your calendar automatically.

> **⚠️ Important:** The Delete Event action must run **in parallel** with the Respond to Event action (not after it). This is because after responding to an event, the event ID becomes unavailable. Running them in parallel ensures both actions can access the original event ID from the trigger.

## ✅ 8. Save and Test

Click **"Save"** in the top right corner.

Your flow is now active and will:
- Run every 5 minutes checking for new events
- Automatically decline meetings on your OOO days
- Send a polite message to the organizer
- Optionally remove the event from your calendar

Congratulations! Your auto-decline flow is ready to go. 🎉
