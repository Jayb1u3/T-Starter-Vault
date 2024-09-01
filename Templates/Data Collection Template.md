---
title: Data Collection - <% tp.date.now("YYYY-MM-DD") %>
data_type: <% await tp.system.prompt("Enter the type of data (e.g., survey, interview, experiment):") %>
project: <% await tp.system.prompt("Enter the project name:") %>
tags: [data, collection]
---

# Data Collection Details

- **Date:** <% tp.date.now("YYYY-MM-DD") %>
- **Location:** <% await tp.system.prompt("Enter the location of data collection (if applicable):") %>
- **Participants:** <% await tp.system.prompt("Enter the number or details of participants (if applicable):") %>
- **Method:** <% await tp.system.prompt("Describe the method of data collection:") %>

# Raw Data
<% await tp.system.prompt("Paste or describe your raw data here:") %>

# Observations
- Observation 1
- Observation 2
- Observation 3

# Notes & Reflections
<% await tp.system.prompt("Enter any reflections or notes on the data collection process:") %>