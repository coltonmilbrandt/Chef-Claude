---
name: showmeprints
description: Open the recipe PDFs folder in Finder. Use to view or manually print exported recipes.
---

# Show Me Prints Skill

Opens the exported recipe PDFs folder in Finder for easy access.

## Invocation
Run `/showmeprints` after `/print` has exported recipes to PDF.

## Core Workflow

### 1. Find Latest Exports
- Look in `print-these-recipes/` for the most recent date folder
- Verify PDFs exist

### 2. Open in Finder
```bash
open print-these-recipes/YYYY-MM-DD/
```

### 3. Confirm
Tell user the folder is open.

## Example Session

```
User: /showmeprints

Claude: Opening print-these-recipes/2025-01-05/ in Finder...

✓ Opened folder with 5 recipe PDFs

Tip: Select all (⌘A) and press ⌘P to print them all at once!
```

## Error Handling

- **No PDFs found**: Prompt user to run `/print` first
- **Folder doesn't exist**: Create it or prompt user to export recipes

## Notes

- Opens the most recent export folder by date
- User can preview PDFs with Quick Look (spacebar)
- For bulk printing: select all → ⌘P
