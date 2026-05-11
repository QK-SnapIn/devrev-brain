---
title: Code node
devrev_id: ART-23382
parent_directory: Workflow engine
translation_group: 69lsqcvI
modified_date: "2026-02-24T08:11:08.42Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/69lsqcvI"
tags: []
top_category: Computer by DevRev
wiki_match: entities/incident
match_score: 0.471
last_updated: 2026-05-11
---

# Code node

The Code node is a powerful workflow component that enables you to write and execute custom Python code directly within your DevRev workflows. It bridges the gap between no-code automation and full programmatic control, giving you the flexibility to implement complex logic, data transformations, and custom business rules without leaving the workflow builder.

Use the Code node when native workflow nodes don't provide the flexibility you need.

|  |  |  |
| --- | --- | --- |
| **Scenario** | **Operation** | **Example** |
| Data transformation | Reshape, filter, merge, or restructure data between workflow steps | Convert "tag1,tag2,tag3" into ["tag1", "tag2", "tag3"], or merge first name + last name into a formatted greeting |
| Complex calculations | Perform math, date arithmetic, or scoring that native nodes can't handle | Calculate SLA deadline by adding business hours to creation time, or compute a priority score from severity × customer tier |
| Text processing | Extract patterns, clean input, or parse unstructured text | Pull all email addresses from a ticket body using regex, or strip @mentions before sending to an external system |
| Custom business logic | Implement organization-specific rules that don't fit standard nodes | Route tickets based on a combination of keywords + customer segment + time of day |
| Dynamic generation | Create computed values on the fly | Generate a reference number like TKT-2024-001234 or build a custom notification message with conditional sections |

When a workflow execution reaches a Code node:

1. The workflow engine collects input values you've configured (mapped from previous steps).
2. Your Python code executes in a secure, sandboxed environment.
3. The run function receives inputs as a dictionary and returns JSON outputs.
4. Returned values become available to downstream nodes (if defined in the output schema).

## Node configuration

The Code node has three main configuration areas.

### Code editor

Write your Python code in the code editor. Your code should be structured within a run function that will be executed by the workflow engine.

```
def run(inputs):
     # your code logic here
     result="Hello, World!"
     return {"output":"result"}
```

### Input values

Define the input parameters your code will receive from previous workflow steps. Input values are passed to your run function as a dictionary.

* Input values are optional: You can create a Code node without any inputs if your logic doesn't depend on previous step outputs
* Access input values using the inputs dictionary: inputs["variable\_name"] where you have defined variable\_name as an input value. E.g. In the following example, "input\_Variable" has been defined as an input

### Output values

Define the output schema for values your code will return.

⚠️ **Important:** You must define output schema for output values to be available to subsequent workflow steps. If you don't define an output schema, output values will not be accessible downstream even if your code returns it.

In the following example, "output\_variable" has been defined as an output of type text

![Screenshot 2026-01-28 at 2.53.19 PM.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/7888946&key=563e2e5e37e34f222f25498e431672a383688132c4da6375cfe1a0bf549a80a7)

## Get started

### Step 1: Add a Code node to a workflow

1. Open your workflow in the DevRev workflow builder
2. Go to the point in your workflow where you need custom logic
3. Click the + button to add a new node
4. Select Execute Code node from the available node types
5. The node will appear on your canvas, ready for configuration

**Tip**: Position your Code node after any nodes whose outputs you'll need to process. The Code node can access outputs from any upstream node in the workflow.

### Step 2: Configure input values

Input values allow your code to receive data from previous workflow steps. This is how you pass ticket information, user data, or any other workflow context into your Python code.

1. Click your Code node to open the configuration panel
2. Navigate to the Input Values section
3. Configure each input:

   * Name: A descriptive identifier (e.g., ticket\_title, customer\_email). This becomes the key you'll use in your code.
   * Value: Use the variable selector to map data from previous nodes
4. Click on “Add value” for more than one input value

**Note**: Input values are only meant for variables, set constants directly in the code.

Example: Setting Up Inputs for Ticket Processing

If you're processing a ticket, you might configure these inputs:

|  |  |  |
| --- | --- | --- |
| **Input name** | **Mapped to** | **Purpose** |
| ticket\_title | {{trigger.ticket.title}} | The ticket's title text |
| ticket\_description | {{trigger.ticket.body}} | The full ticket description |
| ticket\_severity | {{trigger.ticket.severity}} | Current severity level |
| reporter\_email | {{trigger.ticket.reported\_[by.email](http://by.email)}} | Email of who reported it |

Once configured, access your inputs in the run function using the input\_values dictionary:

```
def run(inputs):
    # Direct access (raises KeyError if missing)
    title = inputs["ticket_title"]
    
    # Safe access with default value (recommended)
    description = inputs.get("ticket_description", "")
    severity = inputs.get("ticket_severity", "low")
    
    # Your processing logic here
    return {"output": "processed"}
```

**Best Practice:** Always use .get() with a default value to handle cases where an input might be missing or null. This prevents your code from failing unexpectedly.

### Step 3: Write Your Python code

The code editor is where you implement your custom logic. Your code must follow a specific structure to work correctly within the workflow.

Every Code node must have a run function that:

* Accepts a single parameter called inputs (a dictionary)
* Returns a dictionary containing your output values

```
def run(input_values):
    # 1. Extract inputs
    my_data = input_values.get("my_input", "default")

    # 2. Process data
    result = my_data.upper()

    # 3. Return outputs as a dictionary
    return {"processed_data": result}
```

**Python libraries**

You can import allowed libraries at the top of your code, outside the run function:

```
import re
import json
from datetime import datetime, timedelta

def run(input_values):
    # Now you can use re, json, datetime, etc.
    text = input_values.get("text", "")
    emails = re.findall(r'[\w\.-]+@[\w\.-]+\.\w+', text)

    return {
        "found_emails": emails,
        "processed_at": datetime.now().isoformat()
    }
```

**Python libraries**

External package installation (pip) is not supported. Only pre-installed libraries are available.

The following Python libraries are available for use in your code:

|  |  |
| --- | --- |
| **Library** | **Description** |
| json | JSON parsing and serialization |
| datetime | Date and time operations (datetime, timedelta, timezone) |
| re | Regular expressions for pattern matching |
| math | Mathematical functions (sqrt, factorial, sin, cos, etc.) |
| requests | HTTP library for making API requests (third-party, explicitly installed) |
| collections | Specialized container datatypes (Counter, defaultdict, deque, OrderedDict, namedtuple) |
| itertools | Functions creating iterators for efficient looping (chain, cycle, permutations, combinations) |
| functools | Higher-order functions and operations on callable objects (reduce, partial, lru\_cache) |
| string | Common string operations and constants (ascii\_letters, digits, punctuation) |
| random | Generate pseudo-random numbers and selections |
| decimal | Decimal fixed-point and floating-point arithmetic |
| fractions | Rational number arithmetic |
| statistics | Statistical functions (mean, median, stdev, variance) |
| typing | Type hints support (List, Dict, Optional, Union, etc.) |
| enum | Support for enumerations |
| copy | Shallow and deep copy operations |
| pprint | Pretty-print data structures |
| textwrap | Text wrapping and filling |
| bisect | Array bisection algorithms for sorted lists |
| heapq | Heap queue algorithm (priority queue) |
| array | Efficient arrays of numeric values |
| time | Time access and conversions (time(), sleep() - limited by timeout) |
| hashlib | Secure hash and message digest algorithms (SHA, MD5, etc.) |
| hmac | Keyed-hashing for message authentication |
| secrets | Generate cryptographically strong random numbers |
| base64 | Base16, Base32, Base64, Base85 data encodings |
| binascii | Convert between binary and ASCII |
| struct | Pack and unpack primitive C datatypes |
| codecs | Codec registry and base classes for encoding/decoding |
| uuid | UUID objects according to RFC 4122 |
| urllib | URL handling modules (urllib.parse, urllib.request) |
| html | HTML manipulation utilities (html.escape, html.unescape) |
| xml | XML processing (xml.etree.ElementTree, xml.dom, xml.sax) |
| csv | CSV file reading and writing |
| configparser | Configuration file parser (INI format) |
| zipfile | Work with ZIP archives |
| tarfile | Read and write tar archive files |
| gzip | Support for gzip files |
| bz2 | Support for bzip2 compression |
| lzma | Compression using the LZMA algorithm |
| zoneinfo | IANA time zone support |
| io | Core tools for working with streams (StringIO, BytesIO) |
| dataclasses | Data class decorator and functions |
| operator | Standard operators as functions |
| keyword | Testing for Python keywords |
| warnings | Warning control |
| contextlib | Utilities for with-statement contexts |
| abc | Abstract base classes |

The following Python libraries are blocked for use in your code. This list is not exhaustive:

* os
* sys
* subprocess
* shutil
* pathlib
* multiprocessing
* threading
* concurrent
* thread
* pickle

**Error handling**

Implement try-except blocks to handle potential errors gracefully:

```
import json
def run(inputs):
    try:
        data = inputs.get("json_string", "{}")
        parsed = json.loads(data)
        return {
            "success": True,
            "parsed_data": parsed,
            "error": None
        }
    except json.JSONDecodeError as e:
        return {
            "success": False,
            "parsed_data": None,
            "error": f"Invalid JSON: {str(e)}"
        }
```

### Step 4: Define output values

This step is critical. Your code may return data, but that data is only available to downstream nodes if you explicitly define it in the output schema.

The workflow engine uses the output schema to:

* Know what data to expect from your code
* Make those values available in the variable selector for subsequent nodes
* Validate the data types of returned values

**Adding output values**

1. In the Code node configuration, go to Output Schema.
2. Click Add Field for each value your code returns.
3. For each output, specify the following:

   * Name: Must exactly match the key in your return dictionary
   * Type: The data type of the value

**Data type mapping**

|  |  |
| --- | --- |
| **Your code returns** | **Select this type** |
| "hello" (Text) | Text |
| 42 or 3.14 (number) | Number |
| True or False | Boolean |
| ["a", "b", "c"] | Array |
| 2026-01-28T18:08:38+0000 | Timestamp |
| Object ID ( TKT-1 ) | ID |

Example: Complete input/output configuration

```
def run(inputs):
    text = inputs.get("description", "")

    word_count = len(text.split())
    is_long = word_count > 100
    keywords = ["urgent", "critical", "asap"]
    found_keywords = [kw for kw in keywords if kw in text.lower()]

    return {
        "word_count": word_count,
        "is_long_description": is_long,
        "urgent_keywords": found_keywords
    }
```

**Output schema**

|  |  |
| --- | --- |
| **Output Name** | **Type** |
| word\_count | Number |
| is\_long\_description | Boolean |
| urgent\_keywords | Array of Text |

### Step 5: Test your code

Before deploying your workflow to production, thoroughly test your Code node.

1. Click the Test button in the Code node configuration
2. Provide sample values for each input
3. Run the test and verify that values match your expectations.

## Runtime limits

|  |  |  |
| --- | --- | --- |
| **Limit** | **Value** | **Description** |
| Maximum timeout | 120 seconds (2 minutes) | Maximum execution time for your code |
| Default timeout | 30 seconds | Default execution time |
|  |  |  |
| Memory limit | 256MB | Maximum memory allocation |
| Output + log size limit | 512KB | Maximum size of returned data and logs |

You can configure the timeout in the Advanced settings of the Code node. The timeout value must be:

* Greater than or equal to the minimum timeout
* Less than or equal to 120 seconds

## Code examples

### Example 1: Simple text transformation

Use case: Convert a ticket title to uppercase

Input values:

* ticket\_title (string): The title from a ticket

Output values:

* formatted\_title (string): The uppercase title

```
def run(input_values):
    title = input_values.get("ticket_title", "")
    formatted = title.upper()

    return {
        "formatted_title": formatted
    }
```

### Example 2: Generate multiple timestamps

Use case: Generate timestamps for the last 5 days (no input required)

Input values: None

Output values:

* timestamps (array): List of ISO-formatted timestamps

```
from datetime import datetime, timedelta

def run(input_values):
    today = datetime.now()
    timestamps = []

    for i in range(5):
        date = today - timedelta(days=i)
        timestamps.append(date.isoformat())

    return {
        "timestamps": timestamps
    }
```

### Example 3: Extract and clean text data

Use case: Extract emails and clean text from a conversation message (remove mentions, extract key content)

Input values:

* message\_text (string): Raw message content

Output values:

* extracted\_emails (array): List of email addresses found
* cleaned\_text (string): Text with mentions removed
* has\_emails (boolean): Whether emails were found

```
import re

def run(input_values):
    text = input_values.get("message_text", "")

    # Extract all email addresses
    email_pattern = r'[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}'
    emails = re.findall(email_pattern, text)

    # Remove @mentions (e.g., @username)
    cleaned = re.sub(r'@\w+', '', text)

    # Remove extra whitespace
    cleaned = ' '.join(cleaned.split())

    return {
        "extracted_emails": emails,
        "cleaned_text": cleaned,
        "has_emails": len(emails) > 0
    }
```

### Example 4: Conditional logic based on input

Use case: Determine routing based on ticket severity

Input values:

* severity (string): Ticket severity level

Output values:

* priority\_score (number): Calculated priority
* escalate (boolean): Whether to escalate
* team (string): Assigned team

```
def run(input_values):
    severity = input_values.get("severity", "low").lower()

    severity_scores = {
        "critical": 100,
        "high": 75,
        "medium": 50,
        "low": 25
    }

    score = severity_scores.get(severity, 25)
    escalate = score >= 75

    if score >= 75:
        team = "tier-2-support"
    elif score >= 50:
        team = "tier-1-support"
    else:
        team = "general-support"

    return {
        "priority_score": score,
        "escalate": escalate,
        "team": team
    }
```

### Example 5: String manipulation and formatting

Use case: Format a notification message with dynamic content

Input values:

* customer\_name (string): Customer's name
* ticket\_id (string): Ticket identifier
* issue\_summary (string): Brief issue description

Output values:

* notification\_message (string): Formatted message
* subject\_line (string): Email subject

```
def run(input_values):
    name = input_values.get("customer_name", "Customer")
    ticket_id = input_values.get("ticket_id", "N/A")
    summary = input_values.get("issue_summary", "No summary provided")

    # Truncate summary if too long
    if len(summary) > 100:
        summary = summary[:97] + "..."

    message = f"""Hello {name},

Thank you for contacting support. Your ticket #{ticket_id} has been received.

Issue Summary: {summary}

Our team will review your request and respond within 24 hours.

Best regards,
Support Team"""

    subject = f"[Ticket #{ticket_id}] Your support request has been received"

    return {
        "notification_message": message,
        "subject_line": subject
    }
```

### Example 6: Array processing

Use case: Finding unique emails from a list of emails

Output values:

* unique (array): unique emails

```
def run(inputs):
# Remove duplicate email addresses
    emails = ["alice@example.com", "bob@example.com", "alice@example.com"]

    unique = list(set(emails))
    return {"unique":unique}
# Returns: ["alice@example.com", "bob@example.com"]Troubleshooting
```

### Issue: Output values not appearing in subsequent nodes

*Cause*: Output values not defined in the output schema.

*Solution*: Ensure every key you return in your code is also defined in the Output Values configuration of the node.

```
# ❌ Wrong - returning value not in schema
return {"my_result": value}  # But "my_result" not defined in Output Values

# ✅ Correct - define "my_result" in Output Values section first
return {"my_result": value}
```

### Issue: Code execution timeout

*Cause*: Code takes longer than the configured timeout to execute.

*Solution*:

* Optimize your code for performance
* Avoid infinite loops
* Increase timeout in Advanced settings (max 120 seconds)
* Consider breaking complex operations into multiple Code nodes

### Issue: Import errors

*Cause*: Trying to import a library that is not available.

*Solution*: Only use libraries from the allowed list. External packages cannot be installed.

### Issue: Input values returning None

*Cause*: Incorrect key name or input not properly mapped.

*Solution*:

* Verify the input key name matches exactly (case-sensitive)
* Use .get() method with default values for safer access
* Check that the input is properly connected in the workflow

```
# ✅ Safe access with default value
value = input_values.get("my_key", "default")
```

### Issue: JSON parsing errors

*Cause*: Attempting to parse invalid JSON or accessing data before parsing.

*Solution*: Add error handling and type checking.

```
import json

def run(input_values):
    raw_data = input_values.get("data", "{}")

    try:
        if isinstance(raw_data, str):
            parsed = json.loads(raw_data)
        else:
            parsed = raw_data
    except json.JSONDecodeError:
        parsed = {}

    return {"parsed_data": parsed}
```

### Issue: Rate limiting errors

*Cause*: Making too many API calls or AI requests in a loop.

*Solution*:

* Reduce the number of operations
* Add delays between requests if needed
* Consider using batch operations when available

## Best practices

* Always use .get() for dictionary access: Prevents KeyError exceptions.
* Define all outputs in the schema: Required for values to be accessible downstream.
* Add type checking: Validate input types before processing.
* Keep code focused: One Code node should do one thing well.
* Use meaningful variable names: Makes debugging easier.
* Handle edge cases: Empty inputs, null values, unexpected types.
* Test with sample data: Verify logic before deploying.

## Source
- DevRev support article [Code node](https://support.devrev.ai/en-US/devrev/article/69lsqcvI) (ART-23382)
