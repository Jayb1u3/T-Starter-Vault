---
title: Meeting Notes - <% tp.date.now("YYYY-MM-DD") %>
attendees: <% await tp.system.prompt("List the attendees:") %>
project: <% await tp.system.prompt("Enter the project or topic of the meeting:") %>
tags: [meeting, notes]
---

# Agenda

1. Agenda Item 1
2. Agenda Item 2
3. Agenda Item 3

# Meeting Notes

- **Discussion Point 1:** 
- **Discussion Point 2:** 
- **Discussion Point 3:** 

# Action Items
1. **Task:** <% await tp.system.prompt("Describe the task:") %>
   - **Assigned to:** <% await tp.system.prompt("Who is responsible for this task?") %>
   - **Deadline:** <% await tp.system.prompt("Enter the deadline:") %>
2. **Task:** 
   - **Assigned to:** 
   - **Deadline:** 

# Next Meeting
- **Date:** <% await tp.system.prompt("Enter the date of the next meeting:") %>
- **Location:** <% await tp.system.prompt("Enter the location (or Zoom link) for the next meeting:") %>