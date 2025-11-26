# TeamSync Assistant - Quick Reference Guide

## 🎯 Quick Start

### Bot Commands
```
/hello                  → Welcome message
/help                   → All available commands
/schedule-meeting       → Schedule a team meeting
/standup               → Submit daily standup
/task-status           → View your tasks
/team-report           → Weekly analytics
```

---

## 🔧 Main Functions by Category

### Meeting Management
```deluge
scheduleMeeting(title, description, attendees, timezone, duration)
findAvailableSlots(attendees, timezone, numSlots)
cancelMeeting(meetingId)
rescheduleMeeting(meetingId, newDate, newTime)
sendMeetingReminder(meetingId, minutesBefore)
```

### Standup Tracking
```deluge
storeStandup(standup)
getStandupsForDate(date)
analyzeStandupSentiment(standup)
generateStandupReport(date)
sendStandupReminders(teamMembers, time)
getStandupStatistics(userId, daysBack)
```

### Task Management
```deluge
getUserTasks(userId, status)
getTeamTasks(teamId, status)
createTask(task)
updateTaskStatus(taskId, newStatus)
assignTask(taskId, assigneeId, assignedBy)
getTaskStatistics(teamId)
getOverdueTasks(teamId)
```

### Analytics
```deluge
generateTeamAnalytics(teamId, periodDays)
analyzeTaskMetrics(teamId, periodDays)
analyzeMeetingMetrics(teamId, periodDays)
analyzeStandupMetrics(teamId, periodDays)
calculateProductivityScore(taskMetrics, meetingMetrics, standupMetrics)
analyzeTeamMorale(teamId, periodDays)
identifyBottlenecks(teamId, periodDays)
generateRecommendations(analytics)
```

### Notifications
```deluge
sendNotification(notification)
sendBulkNotifications(notifications)
sendCliqMessage(userId, message, type)
sendChannelMessage(channelId, message, messageType)
createTaskNotification(taskId, userId, action)
createMeetingNotification(meetingId, userId, action)
createStandupNotification(userId)
```

### API Integrations
```deluge
createCalendarEvent(accessToken, title, description, startTime, endTime, attendees)
getProjectTasks(accessToken, projectId)
createProjectTask(accessToken, projectId, taskName, assignee, dueDate)
getCRMContacts(accessToken, moduleType)
insertCreatorRecord(accountName, workspaceName, formName, data)
```

### Utilities
```deluge
formatDate(date, format)
convertTimezone(time, fromTz, toTz)
truncateString(string, maxLength, suffix)
toTitleCase(string)
parseCommandArgs(commandString)
isValidEmail(email)
removeDuplicates(list)
sortByKey(list, key, descending)
```

### Logging & Errors
```deluge
debugLog(message, module)
infoLog(message, module)
warningLog(message, module)
errorLog(message, module)
handleError(code, message, stackTrace, function, severity)
handleAPIError(code, apiName, message)
handleDatabaseError(code, message, query)
```

---

## 📊 Data Models Quick Reference

### Task
```deluge
createTaskObject(title, description, assignee, dueDate, priority, project)
// Returns: {id, title, status, priority, assignee, dueDate, ...}
```

### Meeting
```deluge
createMeetingObject(title, description, startTime, endTime, attendees, timezone)
// Returns: {id, title, attendees, status, remindersSet, ...}
```

### Standup
```deluge
createStandupObject(userId, date, yesterday, today, blockers)
// Returns: {id, userId, sentiment, submittedAt, ...}
```

### TeamMember
```deluge
createTeamMemberObject(name, email, timezone, skills, department)
// Returns: {id, name, skills, workload, availability, ...}
```

### Notification
```deluge
createNotification(userId, type, title, message, actionUrl)
// Returns: {id, userId, type, status, isRead, ...}
```

---

## 🎨 Response Formatting

### Simple Text Response
```deluge
buildResponse("Your message here")
```

### Card Response
```deluge
buildCardResponse("Title", "Description", "#3498DB")
```

### Form Response
```deluge
formFields = List();
formFields.add(Map("name", "fieldName", "label", "Field Label", "type", "text", "required", true));
buildFormResponse(formFields)
```

### Error Response
```deluge
buildErrorResponse("Error description")
```

---

## 📅 Scheduled Tasks

| Task | Time | Frequency | Module |
|------|------|-----------|--------|
| Daily Standup Reminder | 9:00 AM | Daily | schedulers.deluge |
| Weekly Team Report | 10:00 AM Mon | Weekly | schedulers.deluge |
| End-of-Day Summary | 6:00 PM | Daily | schedulers.deluge |
| Task Reminders | Every hour | Hourly | schedulers.deluge |
| Meeting Reminders | Every 30 min | 30 minutes | schedulers.deluge |

---

## 🔌 API Endpoints

### Zoho Calendar
```
Base: https://www.zohoapis.com/calendar/v2
GET    /calendars/primary/events
POST   /calendars/primary/events
PUT    /calendars/primary/events/{eventId}
```

### Zoho Projects
```
Base: https://www.zohoapis.com/projects/v3
GET    /projects/{projectId}/tasks
POST   /projects/{projectId}/tasks
PUT    /projects/{projectId}/tasks/{taskId}
GET    /projects/{projectId}/members
```

### Zoho CRM
```
Base: https://www.zohoapis.com/crm/v3
GET    /Contacts
POST   /Contacts
PUT    /Contacts/{recordId}
```

### Zoho Creator
```
Base: https://www.zohoapis.com/creator/v2
GET    /accounts/{accountId}/{workspaceId}/api/json/{tableName}
POST   /accounts/{accountId}/{workspaceId}/api/json/{tableName}
PUT    /accounts/{accountId}/{workspaceId}/api/json/{tableName}/{recordId}
```

---

## 🎯 Productivity Score Calculation

```
Score = (TaskCompletion × 0.4) + (Efficiency × 0.3) + (Standup × 0.2) + (FocusTime × 0.1)

Score Range:
80-100  → Excellent 🟢
60-79   → Good 🟡
40-59   → Average 🟠
20-39   → Below Average 🔴
0-19    → Needs Improvement ⚫
```

---

## 🐛 Common Issues & Solutions

| Issue | Solution |
|-------|----------|
| Bot not responding | Check webhook URL and OAuth tokens |
| Meetings not creating | Verify Calendar API access and attendee emails |
| Standups not storing | Check Creator table exists and connection |
| Analytics not calculating | Ensure task data exists and dates are valid |
| Reminders not sending | Verify Cliq API access and user IDs |

---

## 📁 File Organization

```
Each Deluge file handles specific concerns:

data_models.deluge          → All data structures
utils.deluge                → Reusable utility functions
api_integrations.deluge     → All Zoho API calls
bot_handlers.deluge         → Webhook entry points
slash_commands.deluge       → Command implementations
meeting_scheduler.deluge    → Meeting logic
standup_handler.deluge      → Standup logic
task_tracker.deluge         → Task logic
schedulers.deluge           → Automated tasks
team_analytics.deluge       → Analytics engine
notification_manager.deluge → Notifications
error_handler.deluge        → Error handling
```

---

## 🔐 Security Best Practices

1. **Store credentials** in environment variables, not in code
2. **Validate all inputs** before processing
3. **Check permissions** before accessing resources
4. **Log errors** without exposing sensitive data
5. **Use HTTPS** for all API calls
6. **Implement rate limiting** for public APIs
7. **Refresh tokens** regularly

---

## 📈 Performance Tips

1. Use Creator indexes for fast queries
2. Batch notifications instead of sending individually
3. Cache frequently accessed data
4. Limit API calls with proper pagination
5. Use scheduled tasks instead of real-time processing
6. Clean up old error logs regularly

---

## 🧪 Testing Commands

```
# Test bot is active
/hello

# Test help system
/help

# Test meeting scheduling
/schedule-meeting "Test Meeting" "user@example.com" "2025-11-28 10:00"

# Test standup
/standup

# Test task status
/task-status

# Test report
/team-report
```

---

## 📖 Documentation Files

- `README.md` - Complete implementation guide
- `IMPLEMENTATION_SUMMARY.md` - Project summary
- `QUICK_REFERENCE.md` - This file
- `configuration.deluge` - Configuration settings

---

**Need Help?**
- Check the error logs in Zoho Creator
- Review the README.md in `/docs/`
- Verify API credentials and permissions
- Test individual functions in Deluge console

---

**Version:** 1.0.0 | **Status:** Production Ready ✅
