---
title: Project Management - <% tp.file.title %>
project: <% await tp.system.prompt("Enter the project name:") %>
tags: [project, management]
status: ongoing
---

# Project: <% tp.frontmatter.project %>

## Overview
<% await tp.system.prompt("Provide a brief overview of the project:") %>

## Objectives
1. Objective 1
2. Objective 2
3. Objective 3

## Milestones
- **Milestone 1:** 
  - **Due Date:** <% await tp.system.prompt("Enter the due date:") %>
  - **Status:** <% await tp.system.prompt("Enter the status:") %>
- **Milestone 2:** 
  - **Due Date:** 
  - **Status:** 

## Tasks
1. **Task:** <% await tp.system.prompt("Describe the task:") %>
   - **Assigned to:** 
   - **Deadline:** 
   - **Status:** 
2. **Task:** 
   - **Assigned to:** 
   - **Deadline:** 
   - **Status:** 

## Notes & Next Steps
