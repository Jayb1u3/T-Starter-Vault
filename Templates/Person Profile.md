<%*
// Collecting information
const aliases = await tp.system.prompt("Enter any aliases for the person:");
const location = await tp.system.prompt("Enter the person's location:");
const companyName = await tp.system.prompt("Enter the person's company:");
const title = await tp.system.prompt("Enter the person's title:");
const email = await tp.system.prompt("Enter the person's email:");
const dateLastSpoken = await tp.system.prompt("Enter the date you last spoke with this person:", "YYYY-MM-DD");
const dateMet = await tp.system.prompt("Enter the date you met this person:", "YYYY-MM-DD");
const languages = await tp.system.prompt("Enter the languages the person speaks:");
const personName = await tp.system.prompt("Enter the person's name:");
const job = await tp.system.prompt("Enter the person's job:");
const educationLevel = await tp.system.prompt("Enter the person's education level:");
const biography = await tp.system.prompt("Enter a short biography for the person:");
const phoneNumber = await tp.system.prompt("Enter the person's phone number:");
;

// Constructing the YAML front matter and note content
const content = `---
tags: 
- Person
aliases: [${aliases}]
Location: "${location}"
Company Name: "${companyName}"
Title: "${title}"
Email: "${email}"
Date Last Spoken: "${dateLastSpoken}"
Date Met: "${dateMet}"
Languages: "${languages}"
Creation Date: "${tp.date.now("YYYY-MM-DD")}"
Last Modified: "${tp.file.last_modified_date("YYYY-MM-DD HH:mm")}"
---

# ${personName}

## Basic Information

- **Job**: ${job}
- **Company**: ${companyName}
- **Title**: ${title}
- **Education Level**: ${educationLevel}

## Biography

${biography}

## Contact Information

- **Email**: ${email}
- **Phone Number**: ${phoneNumber}

## Notes
`;

// Outputting the entire constructed content to the note
tR += content;
%>