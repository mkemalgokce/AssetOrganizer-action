# AssetOrganizer Action

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-AssetOrganizer-blue.svg?colorA=24292e&colorB=0366d6&style=flat&longCache=true&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAAOCAYAAAAfSC3RAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAM6wAADOsB5dZE0gAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAERSURBVCiRhZG/SsMxFEZPfsVJ61jbxaF0cRQRcRJ9hlYn30IHN/+9iquDCOIsblIrOjqKgy5aKoJQj4O3EEtbPwhJbr6Te28CmdSKeqzeqr0YbfVIrTBKakvtOl5dtTkK+v4HfA9PEyBFCY9AGVgCBLaBp1jPAyfAJ/AAdIEG0dNAiyP7+K1qIfMdonZic6+WJoBJvQlvuwDqcXadUuqPA1NKAlexbRTAIMvMOCjTbMwl1LtI/6KWJ5Q6rT6Ht1MA58AX8Apcqqt5r2qhrgAXQC3CZ6i1+KMd9TRu3MvA3aH/fFPnBodb6oe6HM8+lYHrGdRXW8M9bMZtPXUji69lmf5Cmamq7quNLFZXD9Rq7v0Bpc1o/tp0fisAAAAASUVORK5CYII=)](https://github.com/marketplace/actions/assetorganizer)

A GitHub Action to detect and analyze unused assets in iOS/macOS projects. This action helps you identify and clean up unused assets in your Xcode projects, reducing app size and maintaining a cleaner codebase.

// ... rest of the existing content ...

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
