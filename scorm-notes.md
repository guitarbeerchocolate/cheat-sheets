# SCORM Cheat Sheet

SCORM (Sharable Content Object Reference Model) is a set of technical standards for eLearning software products, ensuring compatibility across different LMS platforms. This cheat sheet outlines key concepts, the SCORM API, data models, and common functions for working with SCORM.

---

## Table of Contents

- [SCORM Versions](#scorm-versions)
- [SCORM API Overview](#scorm-api-overview)
- [SCORM Data Model](#scorm-data-model)
  - [SCORM 1.2 Data Model](#scorm-12-data-model)
  - [SCORM 2004 Data Model](#scorm-2004-data-model)
- [Common SCORM API Functions](#common-scorm-api-functions)
- [Error Handling](#error-handling)
- [Examples](#examples)
  - [Retrieve Learner’s Score](#retrieve-learner-score-example)
  - [Ending a SCORM Session](#ending-a-scorm-session-example)

---

## SCORM Versions

### SCORM 1.2

- Released in 2001, this is the most widely adopted SCORM version.
- Limited support for tracking learner interactions and content navigation.

### SCORM 2004

- Introduced in 2004 with enhanced tracking capabilities.
- Supports sequencing and navigation, more granular tracking of learner interactions, and greater flexibility with objectives.

---

## SCORM API Overview

SCORM uses a **JavaScript API** that allows content (SCOs) to communicate with the LMS. The API manages data such as the learner’s progress, score, and session time.

Key API methods:

- **Initialize** (`LMSInitialize()` for SCORM 1.2, `Initialize()` for SCORM 2004)
- **Terminate** (`LMSFinish()` for SCORM 1.2, `Terminate()` for SCORM 2004)
- **Get and Set Data** (`LMSGetValue()`, `LMSSetValue()` for SCORM 1.2; `GetValue()`, `SetValue()` for SCORM 2004)

---

## SCORM Data Model

The SCORM data model consists of elements that are used to store and retrieve data. The most common elements include learner information, scores, completion status, and more.

### SCORM 1.2 Data Model

| **Element**                | **Description**                                   |
| -------------------------- | ------------------------------------------------- |
| `cmi.core.student_id`      | The learner's ID.                                 |
| `cmi.core.student_name`    | The learner's name.                               |
| `cmi.core.lesson_location` | Bookmark: the location the learner left off.      |
| `cmi.core.lesson_status`   | Status of the lesson (`completed`, `incomplete`). |
| `cmi.core.score.raw`       | The learner's score (0-100).                      |
| `cmi.core.total_time`      | The total time spent in the course.               |
| `cmi.suspend_data`         | Stores information to resume the session.         |

### SCORM 2004 Data Model

| **Element**             | **Description**                                     |
| ----------------------- | --------------------------------------------------- |
| `cmi.learner_id`        | The learner's unique ID.                            |
| `cmi.learner_name`      | The learner's full name.                            |
| `cmi.location`          | Bookmark: where the learner left off.               |
| `cmi.completion_status` | `completed`, `incomplete`, `not attempted`.         |
| `cmi.success_status`    | `passed` or `failed`.                               |
| `cmi.score.scaled`      | Learner’s score represented as a decimal (0.0-1.0). |
| `cmi.suspend_data`      | Data to resume the session.                         |
| `cmi.interactions`      | Tracks quiz questions and learner interactions.     |

---

## Common SCORM API Functions

| **Function**                | **Description**                                      |
| --------------------------- | ---------------------------------------------------- |
| `LMSInitialize("")`         | Initializes communication with the LMS (SCORM 1.2).  |
| `Initialize("")`            | Initializes communication with the LMS (SCORM 2004). |
| `LMSFinish("")`             | Ends communication with the LMS (SCORM 1.2).         |
| `Terminate("")`             | Ends communication with the LMS (SCORM 2004).        |
| `LMSGetValue(key)`          | Retrieves a value from the LMS.                      |
| `LMSSetValue(key, value)`   | Sends a value to the LMS (e.g., score, completion).  |
| `LMSCommit("")`             | Saves data to the LMS (SCORM 1.2).                   |
| `Commit("")`                | Saves data to the LMS (SCORM 2004).                  |
| `GetLastError()`            | Returns the error code from the last API call.       |
| `GetErrorString(errorCode)` | Returns a human-readable description of the error.   |
| `GetDiagnostic(errorCode)`  | Returns more detailed information on an error.       |

---

## Error Handling

SCORM uses a set of predefined error codes. When a SCORM API function fails, use `GetLastError()`, `GetErrorString()`, and `GetDiagnostic()` to retrieve details.

- `0`: No error.
- `101`: General exception.
- `201`: Invalid argument error.
- `202`: Element cannot have children.
- `301`: Not initialized (API not initialized before calling other functions).

Example for error handling:

```js
var errorCode = scormAPI.GetLastError();
if (errorCode !== "0") {
  console.log(scormAPI.GetErrorString(errorCode));
}
```

---

## Examples

### Retrieve Learner’s Score Example

```js
var learnerScore = scormAPI.LMSGetValue("cmi.core.score.raw");
console.log("Learner's score is: " + learnerScore);
```

### Ending a SCORM Session Example

**For SCORM 1.2:**

```js
scormAPI.LMSFinish("");
```

**For SCORM 2004:**

```js
scormAPI.Terminate("");
```

---

## Best Practices

- **Use Suspend Data**: To support resuming sessions, store and retrieve state information using `cmi.suspend_data`.
- **Test Across LMSs**: SCORM may behave differently on various LMS platforms, so test extensively.
- **Avoid Long Sessions**: Regularly commit data to the LMS to prevent data loss during long sessions (`LMSCommit()` / `Commit()`).
- **Track Progress**: Use `cmi.core.lesson_status` to track learner progress and completion.

---

## Resources

- [SCORM Explained](https://scorm.com/scorm-explained/)
- [SCORM Cloud](https://cloud.scorm.com/)
- [ADL SCORM Documentation](https://adlnet.gov/scorm/)
