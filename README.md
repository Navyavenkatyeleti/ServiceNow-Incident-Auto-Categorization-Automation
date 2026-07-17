# ServiceNow Incident Auto-Categorization Automation

## Overview
This project streamlines ITSM operations by automating incident classification using **ServiceNow Flow Designer**. It eliminates manual triage, reduces human error, and improves incident routing accuracy in a ServiceNow instance.

## Business Challenge
Before this automation, incident categorization was a manual process, leading to:
* **Inconsistent categorization** across the IT team.
* **Delayed resolution** due to incorrect initial assignment.
* **Administrative overhead** for Service Desk managers.

## Technical Implementation
* **Platform**: ServiceNow PDI (Australian Release).
* **Tools**: Flow Designer, Table Administration, and JavaScript.
* **Logic**: Implemented case-insensitive keyword matching using `.toLowerCase()` to ensure robust classification regardless of user input format[cite: 1].

## Key Features
1. **Automated Categorization**: Automatically sets `Category` and `Assignment Group` based on incident keywords (e.g., 'password', 'email', 'laptop', 'VPN')[cite: 1].
2. **Case-Insensitive Processing**: Utilizes server-side scripting to normalize the `short_description` input, ensuring 100% keyword capture regardless of character case[cite: 1].
3. **Optimized Performance**: Built using Flow Designer triggers to ensure minimal database overhead during incident creation[cite: 1].

## JavaScript Logic (Case-Insensitive)
Below is the core script logic implemented to handle case-insensitive keyword matching:

```javascript
/**
 * Script Logic for Incident Auto-Categorization
 * Used in Flow Designer to handle case-insensitive keyword matching.
 */

var desc = fd_data.trigger.current.short_description.toString().toLowerCase();

// Define keywords and their respective categories
var keywords = {
    'password': 'Access',
    'email': 'Software',
    'laptop': 'Hardware',
    'vpn': 'Network'
};

// Check if description contains any of the keywords
for (var key in keywords) {
    if (desc.includes(key)) {
        return true; 
    }
}
return false;
