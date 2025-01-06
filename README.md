# AssetOrganizer Action

A GitHub Action to detect and analyze unused assets in iOS/macOS projects. This action helps you identify and clean up unused assets in your Xcode projects, reducing app size and maintaining a cleaner codebase.

## Features

- 🔍 Detects unused assets in your project
- 📊 Generates detailed reports in multiple formats (Markdown, JSON)
- 🎨 Supports various asset types:
  - Images (.png, .jpg, .jpeg, .gif, .pdf, .svg)
  - Colors (.colorset)
  - Data Sets (.dataset)
- 🗑 Size-based filtering
- 🎯 Asset type filtering

## Usage

Add this action to your workflow:

```yaml
- name: Check Unused Assets
  uses: mkemalgokce/assetorganizer-action@v1
  with:
    project-path: './MyApp'  # Path to your project
    output-format: 'md'      # Output format (md or json)
    min-size: '100KB'        # Optional: Minimum size threshold
    asset-type: 'image'      # Optional: Filter by asset type
```

### Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `project-path` | Path to the project directory to analyze | Yes | `.` |
| `output-format` | Output format (md, json) | No | `md` |
| `min-size` | Minimum size threshold (e.g., 100KB, 1MB) | No | `0` |
| `asset-type` | Asset type to analyze (image, color, data) | No | `all` |

### Outputs

The action will create a report file and upload it as an artifact. You can download the report using the `actions/download-artifact` action:

```yaml
- name: Download Report
  uses: actions/download-artifact@v3
  with:
    name: asset-analysis-report
```

## Example Workflow

Here's a complete example workflow:

```yaml
name: Check Assets

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:  # Manual trigger

jobs:
  check-assets:
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Check Unused Assets
        uses: mkemalgokce/assetorganizer-action@v1
        with:
          project-path: '.'
          output-format: 'md'
          min-size: '100KB'
          
      - name: Download Report
        uses: actions/download-artifact@v3
        with:
          name: asset-analysis-report
```

## Report Format

The analysis report includes:

- 📊 Summary statistics
  - Total number of assets
  - Number of unused assets
  - Total size
  - Size of unused assets
- 📋 Detailed asset information
  - Asset name and type
  - File size
  - Usage status
- ⚠️ Unused assets summary
  - File paths
  - Sizes
  - Asset types

## Requirements

- The workflow must run on `macos-latest`
- Your project must be an iOS/macOS project with asset catalogs

## License

This project is licensed under the MIT License - see the LICENSE file for details. 