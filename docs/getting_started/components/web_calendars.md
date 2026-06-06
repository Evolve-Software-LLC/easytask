---
title: Holiday Calendar Management - EasyTask Documentation
description: Manage holiday calendars in EasyTask to control task execution on non-working days with date ranges, calendar grouping, and automatic scheduler refresh.
keywords:
  - holiday calendar
  - easytask
  - task scheduling
  - non-working days
  - calendar management
---

### 📅 Manage Holiday Calendar

The **Manage Holiday Calendar** module in EasyTask is crucial for controlling task execution around non-working days. When you assign a holiday calendar to a task, the EasyTask Scheduler checks this calendar before executing the task.

✅ **If the day is marked as a holiday, the scheduler will skip running the task** — ensuring that no critical operations, reports, or workflows are executed on holidays when teams may be offline.

This helps:
- Prevent system or business disruptions on public holidays.
- Ensure that dependent downstream systems are not triggered when staff are unavailable.
- Automate “no-run” days without needing to manually disable tasks.

**Example use cases:**
- Skip financial reconciliations on public holidays.
- Pause automated batch jobs on company-wide off days.
- Respect global/regional holiday calendars for multinational teams.

**Interface Details:**   

- **Add Holidays**:   
    - ``Holiday Reason``: Specifies the name or purpose of the holiday.   
    - ``Date Selection``: Allows selecting a specific date or date range.   
    - ``Calendar Name``: Associates the holiday with a specific calendar (e.g., Indian Calendar, US Calendar).   
    - ``Add Holiday Button``: Saves the new holiday entry.   

- **Holidays Table**:   
    - ``Date``: The assigned holiday date.   
    - ``Reason of Holiday``: Description of the holiday.   
    - ``Calendar Name``: The category to which the holiday belongs.   
    - ``Filtering Options``: Filter by date, reason, or calendar.   
    - ``Search & Pagination``: Find specific entries and control display size.   
    - ``Action Column``: Manage or delete holidays.   

**Scheduler Behavior Example:**   

If a task has the attribute:   
```
"calendar": "US Calendar"
```
and `July 4` is marked as a holiday, the scheduler will automatically skip execution on that day.   

- **Add Holidays** ➝ Name, date/range, calendar name.  
- **View Holidays** ➝ Filter/search by date, reason, calendar.  
- **Delete Holiday** ➝ Use 🗑️ icon.

---

## Frequently Asked Questions

**Q: How do holiday calendars interact with task scheduling?**
A: When a task has a calendar assigned (e.g., `"calendar": "US Calendar"`), the scheduler checks this calendar before execution. If the current day is marked as a holiday, the task is automatically skipped without manual intervention.

**Q: Can I create multiple holiday calendars for different regions?**
A: Yes. Holidays are organized by "Calendar Name" (e.g., `US_Holidays`, `EU_Holidays`, `Indian Calendar`). You can assign different calendars to different tasks based on the regional team or business requirements.

**Q: Do I need to restart the scheduler after adding a new holiday?**
A: No. Changes to the holiday calendar trigger an automatic scheduler refresh, so new holidays are immediately respected without requiring a restart.

## Next Steps

- [Web Administration](./web_administration.md)
- [Web Scheduler](./web_scheduler.md)
- [Scheduler Events](./scheduler_events.md)
