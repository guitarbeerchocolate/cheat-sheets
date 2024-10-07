# SCORM Cheat Sheet

SCORM (Sharable Content Object Reference Model) is a set of technical standards for eLearning software products. It ensures that content can be shared across different Learning Management Systems (LMS) in a standardized format.

---

## Table of Contents

- [What is SCORM?](#what-is-scorm)
- [SCORM Versions](#scorm-versions)
  - [SCORM 1.2](#scorm-12)
  - [SCORM 2004](#scorm-2004)
- [SCORM Components](#scorm-components)
  - [Content Package](#content-package)
  - [Manifest File (imsmanifest.xml)](#manifest-file-imsmanifestxml)
- [SCORM API](#scorm-api)
  - [Common SCORM API Functions](#common-scorm-api-functions)
  - [Example: Retrieve Learner's Score](#example-retrieve-learners-score)
  - [Example: Ending the SCORM Session](#example-ending-the-scorm-session)
- [SCORM Data Model](#scorm-data-model)
  - [SCORM 1.2 Data Model](#scorm-12-data-model)
  - [SCORM 2004 Data Model](#scorm-2004-data-model)
- [SCORM Packaging](#scorm-packaging)
- [Testing SCORM Packages](#testing-scorm-packages)
- [SCORM Best Practices](#scorm-best-practices)

---

## What is SCORM?

- **SCORM** is a set of technical standards used for eLearning software products.
- It ensures that digital content (courses, assessments) can work on different LMS platforms.
- SCORM allows the tracking of learners’ progress, scores, completion, and more through a standardized data model.

---

## SCORM Versions

### SCORM 1.2

- Released in 2001 and widely used.
- Simple data model, but lacks advanced tracking.
- Main limitations: Limited sequencing and navigation capabilities.

### SCORM 2004

- Released in 2004 with enhanced features.
- Supports **sequencing** and **navigation controls**.
- Provides improved tracking capabilities (e.g., detailed interactions and objectives).

---

## SCORM Components

### Content Package

- A SCORM package is a **ZIP file** that contains:
  - HTML, JS, or multimedia files for course content.
  - A manifest file (`imsmanifest.xml`) to define the course structure.

### Manifest File (imsmanifest.xml)

- **imsmanifest.xml** is the heart of any SCORM package.
- It defines:
  - Metadata about the course.
  - The structure of the course (modules, lessons, etc.).
  - Resource files and interactions with the LMS.

Example manifest file:

```xml
<manifest>
  <metadata>
    <schema>ADL SCORM</schema>
    <schemaversion>1.2</schemaversion>
  </metadata>
  <organizations>
    <organization>
      <item identifier="Item1">
        <title>Lesson 1</title>
        <resource identifierref="Resource1" />
      </item>
    </organization>
  </organizations>
  <resources>
    <resource identifier="Resource1" href="index.html" />
  </resources>
</manifest>
```

---

## SCORM API

SCORM content interacts with the LMS using JavaScript through a SCORM-compliant API. The API enables tracking of progress, scores, completion, etc.

### Common SCORM API Functions

| **Function**                | **Description**                                                      |
| --------------------------- | -------------------------------------------------------------------- |
| `LMSInitialize("")`         | Initializes communication with the LMS (SCORM 1.2).                  |
| `Initialize("")`            | Initializes communication with the LMS (SCORM 2004).                 |
| `LMSGetValue(key)`          | Retrieves a value from the LMS (e.g., `cmi.core.lesson_status`).     |
| `LMSSetValue(key, value)`   | Sends a value to the LMS (e.g., completion status, learner's score). |
| `LMSCommit("")`             | Saves data to the LMS after `LMSSetValue()` is called.               |
| `LMSFinish("")`             | Ends communication with the LMS (SCORM 1.2).                         |
| `Terminate("")`             | Ends communication with the LMS (SCORM 2004).                        |
| `GetLastError()`            | Returns the error code from the last SCORM operation.                |
| `GetErrorString(errorCode)` | Returns a string describing the error code.                          |

### Example: Retrieve Learner's Score

```js
var score = scormAPI.LMSGetValue("cmi.core.score.raw"); // Retrieve the learner's raw score
console.log("Learner's score: " + score);
```

### Example: Ending the SCORM Session

**For SCORM 1.2**:

```js
scormAPI.LMSFinish(""); // End SCORM session (SCORM 1.2)
```

**For SCORM 2004**:

```js
scormAPI.Terminate(""); // End SCORM session (SCORM 2004)
```

---

## SCORM Data Model

The SCORM data model consists of a collection of data elements (e.g., scores, completion status, time spent) that are exchanged between the LMS and the SCORM content.

### SCORM 1.2 Data Model

| **Data Model Element**     | **Description**                                                              |
| -------------------------- | ---------------------------------------------------------------------------- |
| `cmi.core.student_id`      | The learner's ID in the LMS.                                                 |
| `cmi.core.student_name`    | The learner's full name.                                                     |
| `cmi.core.lesson_status`   | Indicates if the lesson is `completed`, `incomplete`, `passed`, or `failed`. |
| `cmi.core.score.raw`       | The learner's raw score (usually 0-100).                                     |
| `cmi.core.total_time`      | The total time spent in the course.                                          |
| `cmi.core.lesson_location` | Bookmarking: Where the learner last left off.                                |
| `cmi.suspend_data`         | Stores data allowing the learner to resume from where they left off.         |

### SCORM 2004 Data Model

| **Data Model Element**  | **Description**                                                           |
| ----------------------- | ------------------------------------------------------------------------- |
| `cmi.learner_id`        | The learner's unique ID in the LMS.                                       |
| `cmi.learner_name`      | The learner's full name.                                                  |
| `cmi.success_status`    | Indicates if the learner passed or failed (`passed`, `failed`).           |
| `cmi.completion_status` | Indicates if the course is `completed`, `incomplete`, or `not attempted`. |
| `cmi.score.scaled`      | Learner's score represented as a decimal (0.0 to 1.0).                    |
| `cmi.total_time`        | The total time the learner has spent in the course.                       |
| `cmi.location`          | Bookmarking: Stores the learner’s last position in the course.            |
| `cmi.suspend_data`      | Used to allow resuming the course from where the learner left off.        |
| `cmi.interactions`      | Tracks learner interactions (e.g., quiz responses).                       |

---

## SCORM Packaging

SCORM content is packaged in a **ZIP file** containing the following:

1. **imsmanifest.xml** (mandatory): Defines course structure, resources, and metadata.
2. **Course content**: HTML files, JavaScript, multimedia, and any other assets required.
3. **Resources folder**: Contains images, videos, etc.

---

## Testing SCORM Packages

- **SCORM Cloud**: A free tool used to test SCORM packages in a SCORM-compliant environment.
- **LMS Upload**: Upload the SCORM package to the LMS you are using to verify compatibility and tracking.
- **Browser Developer Tools**: Use the console to debug SCORM API calls when testing in an LMS.

---

## SCORM Best Practices

- **Modular Content**: Break content into smaller SCOs (Sharable Content Objects) for reusability.
- **Error Handling**: Always check for errors using `GetLastError()` and handle them properly.
- **Testing**: Test your SCORM package in different LMS environments (SCORM Cloud is great for this).
- **Suspend Data**: Use `cmi.suspend_data` to track learner progress and allow them to resume later.
- **Version Choice**: Choose **SCORM 2004** if you need more detailed tracking (interactions, objectives). Choose **SCORM 1.2** for simpler needs and wider compatibility.

---

## Resources

- [SCORM Explained](https://scorm.com/scorm-explained/)
- [SCORM Cloud](https://cloud.scorm.com/)
- [ADL SCORM Documentation](https://www.adlnet.gov/scorm/)

---

This SCORM cheat sheet provides a quick reference to the SCORM API, data models, and best practices. It will help you get started with SCORM or brush up on key concepts for developing SCORM-compliant courses.
