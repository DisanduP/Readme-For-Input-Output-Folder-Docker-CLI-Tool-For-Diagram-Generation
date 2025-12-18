# Readme-For-Input-Output-Folder-Docker-CLI-Tool-For-Diagram-Generation

# Diagram Converter Workflow Guide

This guide explains how to use the Input and Output folders for organized diagram conversions with the Diagram Converter Tool.

## Folder Structure

```
Diagram-Converter-Tool/
├── Input/           # Markdown documentation files
├── Output/          # Draw.io XML files
├── *.mmd            # Source Mermaid files
└── diagram-cli.js   # CLI tool
```

## Input Folder

**Purpose**: Store generated Markdown documentation files and reference materials.

### Usage Examples

```bash
# Generate Markdown documentation in Input folder
node diagram-cli.js to-markdown auth-system-final.mmd -o Input/auth-system-final-docs.md

# Generate documentation for app navigation
node diagram-cli.js to-markdown app-navigation.mmd -o Input/app-navigation-docs.md

# Batch generate docs for all .mmd files
for file in *.mmd; do
  base=$(basename "$file" .mmd)
  node diagram-cli.js to-markdown "$file" -o "Input/${base}-docs.md"
done
```

### File Naming Convention
- Use `-docs.md` suffix
- Example: `diagram-name-docs.md`

## Output Folder

**Purpose**: Store converted Draw.io XML files for editing and sharing.

### Usage Examples

```bash
# Convert to Draw.io XML in Output folder
node diagram-cli.js to-drawio auth-system-final.mmd -o Output/auth-system-final.drawio

# Convert app navigation flowchart
node diagram-cli.js to-drawio app-navigation.mmd -o Output/app-navigation.drawio

# Batch convert all .mmd files to Draw.io
for file in *.mmd; do
  base=$(basename "$file" .mmd)
  node diagram-cli.js to-drawio "$file" -o "Output/${base}.drawio"
done
```

### File Naming Convention
- Use `.drawio` extension
- Example: `diagram-name.drawio`

## Combined Workflow

### Individual Conversions

```bash
# Convert auth system flowchart
node diagram-cli.js to-drawio auth-system-final.mmd -o Output/auth-system-final.drawio
node diagram-cli.js to-markdown auth-system-final.mmd -o Input/auth-system-final-docs.md

# Convert app navigation
node diagram-cli.js to-drawio app-navigation.mmd -o Output/app-navigation.drawio
node diagram-cli.js to-markdown app-navigation.mmd -o Input/app-navigation-docs.md
```

### Batch Processing

```bash
# Process all .mmd files in current directory
for file in *.mmd; do
  base=$(basename "$file" .mmd)
  echo "Processing $file..."

  # Generate Draw.io file
  node diagram-cli.js to-drawio "$file" -o "Output/${base}.drawio"

  # Generate Markdown documentation
  node diagram-cli.js to-markdown "$file" -o "Input/${base}-docs.md"

  echo "✓ Completed $base"
done
```

### Full Conversion (Alternative)

```bash
# Use full conversion (places both files in same directory)
# Note: This puts both .drawio and -docs.md in the specified directory
node diagram-cli.js convert auth-system-final.mmd -d Output/
```

## Opening Generated Files

### Draw.io Files (Output Folder)
```bash
# Open in web browser
open Output/auth-system-final.drawio

# Or drag into app.diagrams.net
# Or use VS Code Draw.io extension
```

### Markdown Files (Input Folder)
```bash
# Open in VS Code
code Input/auth-system-final-docs.md

# Or any Markdown viewer
open Input/auth-system-final-docs.md
```

## Validation

Always validate your Mermaid files before conversion:

```bash
# Validate syntax
node diagram-cli.js validate auth-system-final.mmd

# Validate all files
for file in *.mmd; do
  echo "Validating $file..."
  node diagram-cli.js validate "$file"
done
```

## Tips

1. **Keep Source Files**: Store your `.mmd` source files in the root directory
2. **Organize Outputs**: Use Input/ for docs, Output/ for editable diagrams
3. **Version Control**: Consider adding Input/ and Output/ to .gitignore if files are generated
4. **Batch Processing**: Use the loop commands above for processing multiple diagrams
5. **Validation First**: Always validate before converting to catch syntax errors

## Quick Reference

```bash
# Setup folders (if needed)
mkdir -p Input Output

# Quick convert current file
node diagram-cli.js to-drawio current.mmd -o Output/current.drawio
node diagram-cli.js to-markdown current.mmd -o Input/current-docs.md

# Batch convert all
for f in *.mmd; do b=$(basename "$f" .mmd); node diagram-cli.js to-drawio "$f" -o "Output/$b.drawio"; node diagram-cli.js to-markdown "$f" -o "Input/$b-docs.md"; done
```</content>
<parameter name="filePath">/Users/disandup/Desktop/cli Perfect/Diagram-Converter-Tool-Flowchart-Perfected/WORKFLOW-README.md
