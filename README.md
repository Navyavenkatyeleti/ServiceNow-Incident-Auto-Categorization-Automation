# Incident Auto-Categorization Flow

## What this project is about
I built this automation to help solve a common frustration in ServiceNow: inconsistent incident data. Often, users submit tickets with varying case styles (e.g., "PASSWORD reset", "password issue", "Password request"), which makes it difficult for automated workflows to trigger correctly. This project uses a clean, efficient script to normalize that data so the system can categorize and assign incidents automatically, no matter how the user types their request.

## How I built it
I wanted to avoid "brute-force" methods like listing every possible case variation. Instead, I focused on a more professional, scalable approach:
*   **Data Normalization**: I used a script at the very start of the flow to convert the `short_description` into a lowercase string.
*   **Defensive Logic**: I added a check to handle empty descriptions, ensuring the flow won't break if a user submits a ticket without a subject.
*   **Clean Conditionals**: By normalizing the data first, the rest of the flow uses simple, readable "If" logic to map keywords like "password" or "email" to the correct category and assignment group.

## Why I took this approach
Instead of relying on custom or non-standard tools, I stuck to core ServiceNow utilities. This makes the flow much easier to maintain, faster to run, and—most importantly—easy for other developers to understand. It demonstrates that I know how to write efficient code that keeps the platform clean and performant.

## How to use it
1.  In Flow Designer, create a new flow triggered by `Incident [incident]` creation or updates.
2.  Use a "Set Flow Variables" action at the start to run the normalization script.
3.  Set up your "If" conditions to evaluate that normalized variable.
4.  Map the results to "Update Record" actions to automate the categorization.
