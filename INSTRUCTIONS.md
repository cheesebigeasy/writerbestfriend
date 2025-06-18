Writer's Best Friend - Complete User Guide

====================
OVERVIEW
====================
Writer's Best Friend is a tool for batch updating XML files using rules. It supports advanced nested tag targeting with XPath-like syntax, perfect for technical writers working with structured documents like MIL-STD-45001D.

====================
GETTING STARTED
====================

1. LOAD XML FILES
   - Click "Select XML File(s)" to choose individual files
   - Click "Select Folder" to load all XML files from a directory
   - Only .xml files will be processed, others are ignored

2. UNDERSTAND YOUR XML STRUCTURE
   - Once files are loaded, check the "XML Structure" panel
   - Shows a tree view of your XML hierarchy with clickable paths
   - Click any path to auto-fill it in the rule editor

3. CREATE UPDATE RULES
   - Use the "Define New Update Rule" section
   - Target tags using simple names, wildcards, or paths

====================
TARGETING SYNTAX
====================

SIMPLE TAGS:
- "status" - Targets all <status> tags anywhere in the document
- "equipment" - Targets all <equipment> tags

WILDCARDS:
- "equipment*" - Matches equipmentCondition, equipmentStatus, etc.
- "*condition" - Matches preCondition, postCondition, etc.
- "data?" - Matches data1, data2, datax, etc.

NESTED PATHS (XPath-like):
- "task/equipment/status" - Only status tags inside equipment inside task
- "*/status" - Status tags inside any parent
- "task/*/condition" - Condition tags at any level inside task
- "maintenanceTask/equipment/condition" - Very specific targeting

====================
CONDITION TYPES
====================

ALWAYS APPLY:
- Rule applies to all matching tags regardless of content

CONTENT EQUALS:
- Rule only applies if tag content exactly matches your value
- Example: Target "status" where content equals "OPERATIONAL"

CONTENT CONTAINS:
- Rule applies if tag content contains your text
- Example: Target tags containing "ENGINE"

CONTENT MATCHES REGEX:
- Advanced pattern matching using regular expressions
- Example: Target content matching "ERROR_\d+" for ERROR_001, ERROR_002, etc.

====================
ACTION TYPES
====================

REPLACE ENTIRE CONTENT:
- Replaces the complete text content of matching tags
- Example: Change "OPERATIONAL" to "REQUIRES_INSPECTION"

REGEX REPLACE IN CONTENT:
- Find and replace using regular expressions within tag content
- Requires both "Search Regex" and "Replacement Value"
- Supports capture groups ($1, $2, etc.)
- Example: Find "Error(\d+)" Replace with "Fixed_Error_$1"

REMOVE TAG:
- Completely removes matching tags from the XML

====================
PROFILE MANAGEMENT
====================

SAVE PROFILES:
- Create reusable rule sets for common XML update tasks
- Enter a profile name (optional) and click "Save Profile"
- Downloads a JSON file you can reload later

LOAD PROFILES:
- Click "Load Profile" and select a previously saved JSON file
- All rules from the profile will be loaded and ready to use
- Useful for standardizing updates across teams

AUTO-SAVE:
- Your current rules are automatically saved to browser storage
- Will be restored when you reload the page

====================
PROCESSING WORKFLOW
====================

1. Create your rules using the form
2. Click "Apply Rules to All Files"
3. Watch file status: ○ pending → ◷ processing → ✓ processed
4. Files with errors show ✗ and display error details
5. Use "Original" and "Modified" buttons to compare changes
6. Click "Download Processed" to get all successfully modified files

====================
MIL-STD-45001D EXAMPLES
====================

UPDATE EQUIPMENT CONDITIONS:
- Target: "maintenanceTask/equipment/condition"
- Condition: "Content Equals" → "OPERATIONAL"  
- Action: "Replace Entire Content" → "REQUIRES_INSPECTION"

UPDATE SAFETY WARNINGS:
- Target: "procedure/*/safetyWarning"
- Condition: "Content Contains" → "CAUTION"
- Action: "Replace Entire Content" → "WARNING - UPDATED PROTOCOL"

REMOVE OUTDATED STATUS:
- Target: "task/equipmentStatus"
- Condition: "Content Equals" → "DEPRECATED"
- Action: "Remove Tag"

STANDARDIZE PART NUMBERS:
- Target: "equipment/partNumber"
- Condition: "Content Matches Regex" → "P(\d+)-OLD"
- Action: "Regex Replace" → Search: "P(\d+)-OLD" Replace: "PN-$1-NEW"

====================
TIPS AND BEST PRACTICES
====================

- Start with simple rules before using complex regex patterns
- Use the XML Structure tree to understand your document hierarchy
- Test rules on a single file before processing large batches
- Save profiles for repetitive tasks (e.g., "Equipment Status Updates")
- Use specific paths when possible to avoid unintended changes
- Always review the "Modified" preview before downloading

====================
TROUBLESHOOTING
====================

XML PARSING ERRORS:
- Check that your XML files are well-formed
- Look for missing closing tags or invalid characters

RULES NOT MATCHING:
- Verify tag names match exactly (case-sensitive)
- Check that your XPath-like paths are correct
- Use wildcards if tag names vary slightly

REGEX ISSUES:
- Test regex patterns in a regex validator first
- Remember to escape special characters (\, +, *, ?, etc.)
- Use capture groups () for complex replacements

PERFORMANCE:
- Large XML files may take longer to process
- Complex regex operations slow down processing
- Consider breaking large rule sets into smaller batches

====================
FILE STATUS INDICATORS
====================

○ = Pending (not yet processed)
◷ = Processing (currently being updated)
✓ = Processed (successfully completed)
✗ = Error (processing failed, see error details)

====================
SUPPORTED FORMATS
====================

- Standard XML (.xml)
- Military standards (MIL-STD-45001D compliant)
- Technical documentation XML
- Configuration files
- Any well-formed XML structure


Create a complete single-page HTML application called "Writer's Best Friend" with the following specifications:

### **Core Functionality:**
Build an XML file processing tool that allows users to:
1. Load multiple XML files or entire folders containing XML files
2. Define custom rules to modify XML content based on conditions
3. Apply these rules to process the XML files
4. Preview original vs modified content side-by-side
5. Download the processed files
6. Save/load rule profiles for reuse

### **Technical Requirements:**
- Single HTML file with embedded CSS and JavaScript
- Use React (via CDN) with Babel for JSX transformation
- Modern, clean UI with Microsoft Fluent Design inspired styling
- Responsive design that works on mobile and desktop
- Local storage for auto-saving rules between sessions

### **User Interface Sections:**

**1. Profile Management**
- Allow users to save current rules as named profiles (JSON download)
- Load previously saved profiles from JSON files
- Auto-save rules to localStorage

**2. File Loading**
- File selector for individual XML files (multiple selection)
- Folder selector to load all XML files from a directory
- File list with status indicators (pending, processing, processed, error)
- File preview pane showing original and modified content

**3. Rule Editor**
- Target tag field with auto-suggestions from discovered XML tags
- Condition logic dropdown with options:
  * Always Apply
  * Content Equals
  * Content Contains  
  * Content Matches Regex
- Action logic dropdown with options:
  * Replace Entire Content with Text
  * Regex Replace in Content
  * Remove Tag
- Validation for regex patterns
- Support for wildcard tag matching (*, ?)

**4. Rule Management**
- List all current rules with edit/delete options
- Show rule summaries with truncated values
- Rule validation and error messaging

**5. Processing & Download**
- Batch process all files with current rules
- Progress indicators during processing
- Download individual files or all files as ZIP
- Error handling for invalid XML

### **Key Features to Implement:**

**XML Processing Logic:**
- Parse XML using DOMParser
- Support wildcard tag matching with regex conversion
- Apply multiple rules in sequence
- Handle regex capture groups ($1, $2, etc.)
- Preserve XML structure and formatting
- Error handling for malformed XML

**Tag Discovery:**
- Automatically extract all unique XML tag names from loaded files
- Provide autocomplete suggestions when typing tag names
- Sort tags alphabetically for easy browsing

**File Management:**
- Track file status (pending/processing/processed/error)
- Generate unique IDs for each file
- Support drag-and-drop functionality
- Filter out non-XML files automatically

**Data Persistence:**
- Auto-save rules to localStorage on every change
- Load saved rules on application startup
- Profile export/import as JSON files

### **Styling Guidelines:**
- Use Segoe UI font family
- Clean, modern interface with subtle shadows and borders
- Color scheme: blues for primary actions, red for danger actions
- Responsive grid layouts
- Consistent spacing and typography
- Visual status indicators with colored dots
- Hover effects and focus states

### **Error Handling:**
- Validate regex patterns in real-time
- Show helpful error messages for invalid XML
- Handle file reading errors gracefully
- Prevent processing without files or rules

### **Code Organization:**
- Separate utility functions for XML processing
- Modular React components for each UI section
- Clean state management with hooks
- Proper event handling and validation

Create a single-page HTML application for processing XML files. Requirements:

TECHNICAL STACK:
- Single HTML file with embedded CSS and JavaScript
- Use React via CDN (18.x) with Babel for JSX
- Modern, clean UI similar to Microsoft Office applications
- No external dependencies beyond React/Babel CDNs

CORE FEATURES:
1. Load multiple XML files from user's computer
2. Create rules to modify XML content (find/replace, remove tags, etc.)
3. Apply rules to all loaded files
4. Preview original vs modified content
5. Download processed files


Create a single-page HTML application for processing XML files. Requirements:

TECHNICAL STACK:
- Single HTML file with embedded CSS and JavaScript
- Use React via CDN (18.x) with Babel for JSX
- Modern, clean UI similar to Microsoft Office applications
- No external dependencies beyond React/Babel CDNs

CORE FEATURES:
1. Load multiple XML files from user's computer
2. Create rules to modify XML content (find/replace, remove tags, etc.)
3. Apply rules to all loaded files
4. Preview original vs modified content
5. Download processed files

UI SECTIONS:
- File loader with drag/drop support
- Rule editor with form fields
- File list with status indicators  
- Preview pane showing before/after content
- Process and download buttons

Start with the basic HTML structure, CSS styling, and file loading functionality. Use a clean, professional design with blue accent colors.
'

"Now add XML parsing functionality that can extract all unique tag names from loaded files"

"Add a rule editor that allows targeting specific XML tags with conditions like 'content contains' or 'content matches regex'"

"Implement the XML processing engine that applies rules to modify file content"

"Add profile save/load functionality using JSON files and localStorage"
UI SECTIONS:
- File loader with drag/drop support
- Rule editor with form fields
- File list with status indicators  
- Preview pane showing before/after content
- Process and download buttons

Start with the basic HTML structure, CSS styling, and file loading functionality. Use a clean, professional design with blue accent colors.
