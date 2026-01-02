<%*
// Collecting information
const aliases = await tp.system.prompt("Enter any aliases: 'example, example'");
const companyName = await tp.system.prompt("Enter the person's company:");
const title = await tp.system.prompt("Enter the person's title:");
const email = await tp.system.prompt("Enter the person's email:");
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
- Contact
aliases: [${aliases}]
Company Name: "${companyName}"
Title: "${title}"
Email: "${email}"
Languages: "${languages}"
Creation Date: "${tp.date.now("YYYY-MM-DD")}"
Last Modified: "${tp.file.last_modified_date("YYYY-MM-DD HH:mm")}"
---

/* –––––––––––––––––––––––––––––––––––––– *
 *            [ BODY OF NOTE ]            * 
 * –––––––––––––––––––––––––––––––––––––– *
 * This section is the body of the note   * 
 * itself. It contains specific sections  * 
 * –––––––––––––––––––––––––––––––––––––– */

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
