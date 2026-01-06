---
name: printit
description: Send recipe PDFs directly to the default printer. Use after /print has exported recipes.
---

# Print It Skill

Sends exported recipe PDFs directly to the printer - no clicking required.

## Invocation
Run `/printit` after `/print` has exported recipes to PDF.

## Core Workflow

### 1. Find Latest Exports
- Look in `print-these-recipes/` for the most recent date folder
- List the PDFs found
- Confirm with user before printing

### 2. Send to Printer
```bash
lpr print-these-recipes/YYYY-MM-DD/*.pdf
```

### 3. Confirm
Report how many recipes were sent to the printer.

## Example Session

```
User: /printit

Claude: Found 5 recipe PDFs in print-these-recipes/2025-01-05/:
1. coconut-curry-chicken.pdf
2. korean-chicken-lettuce-wraps.pdf
3. mexican-chicken-bowl.pdf
4. spicy-ginger-garlic-chicken.pdf
5. thai-basil-chicken-stir-fry.pdf

Sending to printer...

✓ Sent 5 recipes to your default printer!
```

## Error Handling

- **No PDFs found**: Prompt user to run `/print` first
- **No printer configured**: Alert user to set up a default printer in System Preferences
- **Print fails**: Show error message from `lpr`

## Notes

- Uses system default printer
- Each recipe prints as a separate document
- User should ensure printer has paper loaded before running
