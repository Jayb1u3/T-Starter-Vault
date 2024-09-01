## What is a Template?
A **template** is a file that contains **commands**. These files help the user avoid repeating tasks that can be appended to a file for frequent and immediate implementation. 
## What is a Command?
- A **command** starts with the opening tag `< %` and ends with `% >`.

# Key Functions

>Below is a list of Templater's _"key functions."_
#### File Functions
**File Content:**
- `tp.file.content`: Retrieves the current file's content.
  
**File Creation:**
- `tp.file.create_new`: Creates a new file with specified content or template.
  
**File Dates:**
- `tp.file.creation_date`: Retrieves the file's creation date.
- `tp.file.last_modified_date`: Retrieves the file's last modification date.
  
**File Location:**
- `tp.file.folder`: Retrieves the file's folder name.
- `tp.file.path`: Retrieves the file's absolute or relative path.
  
**File Manipulation:**
- `tp.file.rename`: Renames the file.
- `tp.file.move`: Moves the file to a different location.
  
**File Inclusion:**
- `tp.file.include`: Includes content from another file or section.
  
**File Existence:**
- `tp.file.exists`: Checks if a file exists at a specified path.
  
**Metadata:**
- `tp.file.tags`: Retrieves the file's tags.
- `tp.file.title`: Retrieves the file's title.
  
**Cursor Control:**
- `tp.file.cursor`: Sets the cursor position for editing.
- `tp.file.cursor_append`: Appends content after the active cursor.

**Text Selection:**
- `tp.file.selection`: Retrieves the current text selection.


# Using Templater Scripts
### Appending to `tR`

When writing a Templater script, you often need to append the result of a function to the output. The `tR` variable is used for this purpose.

> **Note:** The `tR` variable accumulates all the output that will be inserted into your note when the script runs.

#### Example: Appending Metadata to a Note
Below is an example of a script that prompts the user for metadata and appends it to the note.

**Step-by-Step Guidance:**

1. **Prompt the User:** The script will prompt the user to enter various pieces of metadata such as aliases, name, date of birth, and date of death.
2. **Construct the Metadata:** The inputs are then used to construct the YAML metadata block.
3. **Append to `tR`:** Finally, the metadata block is appended to `tR` for insertion into the note.

**Full Script:**

```javascript

<%*
// Prompt the user for metadata values
const aliases = await tp.system.prompt("Enter aliases");
const name = await tp.system.prompt("Enter name");
const dob = await tp.system.prompt("Enter date of birth");
const dod = await tp.system.prompt("Enter date of death");

// Construct the YAML metadata block
const metaData = `---
aliases: ${aliases}
name: ${name}
dob: ${dob}
dod: ${dod}
tags: 
  - Person
---`;


// Append the metadata block to the note
tR += metaData;
%>
```

> **Key Point:** The `${expression}` syntax is used to insert the value of a variable (e.g., `${aliases}`) into a string.

***
## Templater Commands for File Manipulation

Templater provides several functions to interact with files. Here’s how you can use them.
### Creating New Files

Our first type of templater function is the `tp.file.create_new`. This specific function is used to create new files.

```js
tp.file.create_new(template: TFile ⎮ string, filename?: string, open_new: boolean = false, folder?: TFolder) 
```

**Explanation:**

- `template`: The template file or string to use.
- `filename`: The name of the new file (optional).
- `open_new`: Boolean to decide if the new file should be opened (default is false).
- `folder`: The folder where the new file will be created (optional).

---
## Using Date Functions in Templater
Templater allows you to insert dates into your notes using specific functions.
### Inserting the Creation Date
You can retrieve the file's creation date and format it as needed.

```javascript

<% tp.file.creation_date("YYYY-MM-DD HH:mm") %>

```

> **Tip:** You can customize the date format by adjusting the format string. For example, use `"YYYY-MM-DD"` to omit the time.

### Example: Inserting the Current Day of the Week

```javascript

<% tp.date.now("dddd") %>

```

This will insert the current day of the week (e.g., "Monday").

***
## Using the System Prompt in Templater
The system prompt function allows you to ask the user for input when the template is run.
### Example: Prompt for User Input

```javascript

<% await tp.system.prompt("Enter your text") %>

```

> **Example Usage:** Place this script in a note where you want the user to input text dynamically. The prompt message will be "*Enter your text*."


---

> **NOTE:** Copy and paste any of these script snippets into your note where you want the functionality. 

> **Key Takeaway:** Start simple with the provided scripts, and as you become more comfortable, explore the full range of Templater's capabilities to customize your workflow to fit your needs.

