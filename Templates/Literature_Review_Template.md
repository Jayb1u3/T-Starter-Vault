---
title: <% tp.file.title %>
author: <% await tp.system.prompt("Enter the author(s) of the paper/book:") %>
journal: <% await tp.system.prompt("Enter the journal/conference/book title:") %>
year: <% await tp.system.prompt("Enter the publication year:") %>
doi: <% await tp.system.prompt("Enter the DOI/link (optional):") %>
tags: [literature, review]
---

# Summary
<% await tp.system.prompt("Provide a brief summary of the paper/book:") %>

# Key Points
- **Research Question:** <% await tp.system.prompt("What is the main research question?") %>
- **Methodology:** <% await tp.system.prompt("Briefly describe the methodology:") %>
- **Key Findings:** 
  - Finding 1
  - Finding 2
  - Finding 3

# Critique
<% await tp.system.prompt("Provide your critique or thoughts:") %>

# Relevance to Your Work
<% await tp.system.prompt("How does this work relate to your research?") %>

# References
- [Reference 1]
- [Reference 2]