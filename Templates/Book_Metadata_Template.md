<%*
/*
NOTE: The `tags`, `aliases`, and `related` fields in the YAML front matter are intentionally left empty.

Please fill these out after the script completes to ensure the note is fully categorized and linked.
*/

// Prompt the user to enter the Chapter Title, Author Name, Publisher, and ISBN
const title = await tp.system.prompt("Enter Chapter Title:");
const author = await tp.system.prompt("Enter Author Name:");
const publisher = await tp.system.prompt("Enter Publisher here:");
const isbn = await tp.system.prompt("Enter the ISBN here:");

// Construct the YAML front matter metadata
const metaData = `---
title: ${title}
author: ${author}
publisher: ${publisher}
isbn: ${isbn}
tags:               
aliases:            
related:            
---`;

// Construct the note body with the title as the main heading
const noteBody = `# ${title}`;

// Combine the metadata and the note body
tR += metaData + noteBody;
%>