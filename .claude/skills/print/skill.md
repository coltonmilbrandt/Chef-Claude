---
name: print
description: Export recipes to PDF for printing. Use when the user wants to print recipes from the current meal plan.
---

# Recipe Printer Skill

You are a recipe printing assistant that exports meal plan recipes to nicely formatted PDFs for printing.

## Invocation
This skill is invoked with `/print` after a meal plan has been created.

## Core Workflow

### 1. Find Current Recipes
- Look in the `recipes/` folder for the most recent date folder (format: YYYY-MM-DD)
- List all `.md` recipe files found
- Confirm with user which recipes to print (all by default)

### 2. Create Output Directory
- Create folder: `print-these-recipes/YYYY-MM-DD/` using today's date
- This keeps printed recipes organized by when they were exported

### 3. Export Recipes to PDF
Export each recipe and move to output folder:
```bash
# Create output directory
mkdir -p print-these-recipes/YYYY-MM-DD

# Export all recipes
for f in recipes/YYYY-MM-DD/*.md; do
  npx md-to-pdf "$f" --stylesheet assets/recipe-style.css --pdf-options '{"format": "Letter", "margin": "0.75in"}'
done

# Move PDFs to output folder
mv recipes/YYYY-MM-DD/*.pdf print-these-recipes/YYYY-MM-DD/
```

### 4. Report Results
After export, provide:
- Number of recipes exported
- Location of PDF files
- Offer next steps:
  - `/printit` - send directly to printer
  - `/showmeprints` - open folder in Finder

## Example Session

```
User: /print

Claude: Found 5 recipes from the January 6, 2025 meal plan:
1. Thai Basil Chicken Stir Fry
2. Coconut Curry Chicken
3. Korean Chicken Lettuce Wraps
4. Mexican Chicken Bowl
5. Spicy Ginger Garlic Chicken

Exporting all to PDF...

✓ Created: print-these-recipes/2025-01-05/
✓ Exported 5 recipes

What's next?
- `/printit` - send directly to your printer
- `/showmeprints` - open folder in Finder
```

## Error Handling

- **No recipes found**: Check if /chef has been run first. Prompt user to create a meal plan.
- **md-to-pdf not installed**: Run `npm install` in project directory
- **Export fails**: Check file permissions, retry individual files

## Notes

- PDFs are styled with a clean recipe card format
- Ingredients display in 2 columns for easy scanning
- Instructions have numbered circles for each step
- Source URL is preserved for reference
