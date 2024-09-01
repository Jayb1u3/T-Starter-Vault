# Overview
Dataview is a powerful plugin for Obsidian that enables you to create dynamic views and reports from the metadata in your notes. By adding [[metadata]] to your notes, you can query them using the [Dataview Query Language (DQL)](https://blacksmithgu.github.io/obsidian-dataview/queries/structure/). This allows you to list, filter, sort, or group your data within your vault. Dataview keeps your queries up to date and helps you efficiently manage and aggregate information across your notes.

> *Dataview essentially serves as a live index that allows you to query your notes and their data dynamically.*

# Adding Metadata to Your Pages

For Dataview to query and display your content, the relevant data needs to be indexed. This indexing happens in three main ways: frontmatter, inline fields, and implicit fields.

### What is a "Field"?

A field in Dataview is a key-value pair where the value’s data type determines how it will be handled in queries. Fields can be added to notes, list items, or tasks.

### How Do I Add Fields?

You can add fields to a note in three primary ways:

1. **Frontmatter:** YAML frontmatter at the top of a note is automatically recognized as metadata by Dataview.
2. **Inline Fields:** Metadata can be embedded directly within the content of your note using `Key:: Value` syntax.
3. **Implicit Fields:** Dataview automatically indexes certain fields, such as the file creation date, tags, links, and more.

## Frontmatter

Frontmatter is a block of YAML metadata placed at the beginning of a note, surrounded by `---` at the start and end.

```yaml
---
alias: "document"
last-reviewed: 2021-08-17
thoughts:
  rating: 8
  reviewable: false
---
```

In this example, the note contains fields such as `alias`, `last-reviewed`, and `thoughts`. These fields are automatically available for Dataview queries.

### Handling Multiline Text in YAML

**Handling Multiline Text in YAML:**  

When working with YAML frontmatter, you can store multiline text using the pipe (`|`) operator. This is particularly useful for storing long text, such as a poem or a detailed description.

**Example:**

```yaml

---

poem: |

  Because I could not stop for Death,

  He kindly stopped for me;

  The carriage held but just ourselves

  And Immortality.

author: "[[Emily Dickinson]]"

title: "Because I could not stop for Death"

---

```

In this example, the `poem` field contains multiline text, which Dataview can then query or display.

## Inline Fields

> Inline fields are embedded within the content of your notes using the `Key:: Value` syntax. This approach allows for more natural annotations.

```markdown
Basic Field:: Some random Value
**Bold Field**:: Nice!
```

### Bracketed Inline Fields

When adding metadata to tasks or list items, use bracketed syntax to ensure Dataview correctly identifies the field:

```markdown
- [ ] Send an email to David about the deadline [due:: 2022-04-05].
```

### Mixing Metadata

You can use YAML frontmatter and inline fields together within the same note, giving you the flexibility to annotate your notes in a way that best suits your workflow.

## Field Names and Sanitization

Dataview sanitizes metadata field names to ensure consistency in queries. This includes converting field names to lowercase, replacing spaces with dashes, and removing formatting like bold or italic.

| Metadata Key             | Sanitized Key              | Value                | Data Type      |
|--------------------------|----------------------------|----------------------|----------------|
| Basic Field               | basic-field                | Some random Value    | Text           |
| Bold Field                | bold-field                 | Nice!                | Text           |
| rating                    | rating                     | 9                    | Number         |
| mood                      | mood                       | acceptable           | Text           |
| due                       | due                        | 2022-04-05           | Date           |

> **Important:** When using spaces or special formatting in your field names, refer to the sanitized key in your queries.

### Usage of Emojis and Non-Latin Characters

You can use emojis and non-Latin characters in metadata keys, but there are some limitations:

```markdown
Noël:: Un jeu de console
クリスマス:: 家庭用ゲーム機
[🎅:: a console game]
[xmas🎄:: a console game]
```

When using emojis, enclose the key in square brackets to ensure proper recognition by Dataview.

## Implicit Fields

Even without explicit metadata, Dataview automatically indexes several fields known as implicit fields. These fields are available for querying and include:

| Field Name         | Data Type      | Description                                                          |
| ------------------ | -------------- | -------------------------------------------------------------------- |
| `file.name`        | Text           | The file name as seen in Obsidian's sidebar.                         |
| `file.folder`      | Text           | The path of the folder this file belongs to.                         |
| `file.path`        | Text           | The full file path, including the file's name.                       |
| `file.ext`         | Text           | The file's extension (typically `md`).                               |
| `file.link`        | Link           | A link to the file.                                                  |
| `file.size`        | Number         | The size (in bytes) of the file.                                     |
| `file.ctime`       | Date with Time | The date and time the file was created.                              |
| `file.cday`        | Date           | The date the file was created.                                       |
| `file.mtime`       | Date with Time | The date and time the file was last modified.                        |
| `file.mday`        | Date           | The date the file was last modified.                                 |
| `file.tags`        | List           | A list of all unique tags in the note.                               |
| `file.etags`       | List           | A list of all explicit tags in the note.                             |
| `file.inlinks`     | List           | A list of all incoming links to this file.                           |
| `file.outlinks`    | List           | A list of all outgoing links from this file.                         |
| `file.aliases`     | List           | A list of all aliases for the note as defined via YAML frontmatter.  |
| `file.tasks`       | List           | A list of all tasks in this file.                                    |
| `file.lists`       | List           | A list of all list elements in the file, including tasks.            |
| `file.frontmatter` | List           | The raw values of all frontmatter in the form of key-value pairs.    |
| `file.day`         | Date           | Only available if the file name contains a date or has a Date field. |
| `file.starred`     | Boolean        | Indicates if the file has been bookmarked.                           |

These implicit fields are automatically generated and can be extremely useful when constructing queries.

# Dataview Query Language (DQL)

The **Dataview Query Language (DQL)** is a powerful, SQL-like language used to query and display data from your Obsidian notes. DQL supports various query types and data commands to refine, sort, group, and transform your results.

## Structure of a Query

Every DQL query follows a similar structure and consists of:

- **Query Type:** Specifies the format of the output (e.g., TABLE, LIST, TASK, CALENDAR).
- **Source (FROM):** Defines the set of pages to query.
- **Data Commands:** Filter, sort, group, or limit the results.

### Differences Between DQL and SQL

**Differences Between DQL and SQL:**  

While Dataview Query Language (DQL) is SQL-like, there are important differences that you should be aware of:

1. **No Joins:** DQL does not support joins like SQL. Instead, you work within the scope of a single set of documents.

2. **Simpler Syntax:** DQL is designed to be simpler and more readable, with commands like `WHERE`, `SORT`, and `GROUP BY` performing operations directly on fields.

3. **No Complex Aggregation:** DQL has limited aggregation functions compared to SQL. It focuses on simple calculations like `count()`, `sum()`, and `average()`.

4. **Contextual Queries:** DQL operates within the context of Obsidian’s notes, allowing it to handle fields like `file.mtime` or `file.tags`, which are specific to the note’s metadata.

**Example:** In SQL, you might write:

```sql

SELECT title FROM books WHERE rating > 7 ORDER BY rating DESC;

```

In DQL, the equivalent would be:

```sql

TABLE title
FROM #books
WHERE rating > 7
SORT rating DESC

```

### Example: Basic Table Query

```c
//This query generates a table of books with a rating greater than 7, sorted by rating in descending order.

TABLE title, author, rating
FROM "Books/"
WHERE rating > 7
SORT rating DESC

```

## Query Types

Dataview offers several output formats for queries:

- **TABLE:** Displays data in a tabular format.
- **LIST:** Shows data as a bullet-point list.
- **TASK:** Displays tasks with interactive checkboxes.
- **CALENDAR:** Visualizes data on a calendar.
- **GALLERY:** Displays images in a grid layout.
- **TIMELINE:** Plots events or data points on a timeline.

### Choosing a Source

Additionally to the Query Types, you have several **Data Commands**available that help you restrict, refine, sort or group your query. One of these query commands is the **FROM** statement. `FROM` takes a [source](https://blacksmithgu.github.io/obsidian-dataview/reference/sources) or a combination of [sources](https://blacksmithgu.github.io/obsidian-dataview/reference/sources) as an argument and restricts the query to a set of pages that match your source.

It behaves differently from the other Data Commands: You can add **zero or one** `FROM` data command to your query, right after your Query Type. You cannot add multiple FROM statements and you cannot add it after other Data Commands.

> The `FROM` command restricts the query to a specific set of pages. 
 
**For example:**

```c
//This query lists all pages within the "Books" folder and its sub folders

LIST FROM "Books"

```

```c

//This query lists all pages that include the tag #status/open or #status/wip

LIST 
FROM #status/open OR #status/wip 

```

```css

LIST
FROM (#assignment AND "30 School") 
OR ("30 School/32 Homeworks" AND outgoing([[School Dashboard Current To Dos]]))

```



### Filtering, Sorting, and Grouping

You can refine your query results using the following data commands:

- **WHERE:** Filters notes based on metadata fields.
- **SORT:** Sorts results by a specified field.
- **GROUP BY:** Groups results based on a field.
- **LIMIT:** Limits the number of results returned.

### Advanced DQL Features: *FLATTEN*, Complex *FROM* Statements

DQL offers advanced commands that allow you to manipulate data in more complex ways:

**`FLATTEN`:**  

- The `FLATTEN` command is used to break up a multi-value field (like a list) into individual items. This is particularly useful when you need to treat each item in a list separately.

**Example:**

```c

TABLE L.text AS "List Items"

FROM "Tasks/"

FLATTEN file.lists AS L

WHERE contains(L.text, "important")

```

This query lists all items in task lists that contain the word "important".


**Complex `FROM` Statements:**  

- You can combine multiple sources in the `FROM` statement using logical operators (`AND`, `OR`). This allows you to target specific subsets of your vault with precision.


**Example:**


```c

LIST

FROM (#assignment AND "30 School") OR ("30 School/32 Homeworks" AND outgoing([[School Dashboard Current To Dos]]))

```

  
This query lists pages that either have the `#assignment` tag and are in the "30 School" folder or are linked on the "School Dashboard Current To Dos" page and reside in the "30 School/32 Homeworks" folder.

### Example: Filtering and Sorting

```c
LIST
WHERE due AND due < date(today)
SORT file.ctime DESC
LIMIT 10
```

This query lists the 10 most recently created pages with a `due` date before today.

# Working with Metadata and Field Types

Dataview recognizes several field types, each of which determines how data is rendered and manipulated in queries.

## Field Types

- **Text:** The default catch-all type.
- **Number:** Represents numeric values.
- **Boolean:** Represents `true` or `false`.
- **Date:** Recognized by the ISO8601 format.
- **Duration:** Represents time spans, such as `6 hours` or `4 minutes`.
- **Link:** Represents Obsidian links, e.g., `[[Page]]`.
- **List:** Represents multi-value fields, defined as YAML lists or comma-separated inline fields.
- **Object:** Represents a map of multiple fields under one parent field.

### Literal Values and Durations

**Literal Values:**  

Dataview allows you to use literal values in your queries, particularly when working with dates and durations. Here are some common literals you can use:

- `date(today)`: Represents the current date.

- `date(now)`: Represents the current date and time.

- `date(tomorrow)`: Represents tomorrow's date.

- `date(yesterday)`: Represents yesterday's date.

- `date(sow)`: Start of the current week.

- `date(eow)`: End of the current week.

- `date(som)`: Start of the current month.

- `date(eom)`: End of the current month.

- `date(soy)`: Start of the current year.

- `date(eoy)`: End of the current year.

  

**Durations:**  

Durations represent a span of time and can be used in calculations with dates. Here are some examples of duration literals:

- `dur(1 s)`: One second.

- `dur(3 m)`: Three minutes.

- `dur(1 h)`: One hour.

- `dur(2 d)`: Two days.

- `dur(1 mo)`: One month.

- `dur(1 yr)`: One year.

- `dur(1 s, 2 m, 3 h)`: Three hours, two minutes, and one second.


**Example:** Calculating the time left until an event:

```C

TABLE release-date, date(now) - release-date AS "Time Left"

WHERE release-date > date(now)

```

This query calculates the time left until the release date of an event.

### Dates and Durations

Dataview supports advanced date and duration calculations. You can add durations to dates or compare dates in queries:

```C
TABLE due, date(today) - due AS "Days Left"
WHERE due > date(today)
```

This query calculates the number of days left until a due date.

# Advanced Features

## Inline DQL

Inline DQL allows you to embed dynamic values directly into your notes using `=`, the default prefix for inline queries.

```c
Today is `= date(today)` - `= [[exams]].deadline - date(today)` until exams!
```

This example displays today’s date and the time left until exams.

## Dataview JS

For more complex queries, you can use DataviewJS, which allows you to write queries using JavaScript.

```cs
```dataviewjs

let pages = dv.pages("#books and -#books/finished").where(b => b.rating >= 7);
for (let group of pages.groupBy(b => b.genre)) {
    dv.header(3, group.key);
    dv.list(group.rows.file.name);
}
```

DataviewJS provides full access to the JavaScript API, enabling you to create complex and customized views.

# References and Resources
- [Dataview Documentation](https://blacksmithgu.github.io/obsidian-dataview/)
