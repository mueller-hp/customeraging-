# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hebrew-language customer aging dashboard for debt collection management. It's a single-file HTML application that uses React, Tailwind CSS, and Chart.js to provide interactive analytics for customer debt aging data.

## Architecture

### Single-File Architecture
- **Main Application**: `index.html` - Complete dashboard application with embedded React components
- **Data Format**: JSON files with Hebrew field names for customer debt data
- **Storage**: Browser localStorage for data persistence
- **Deployment**: GitHub Pages ready (no build process required)

### Core Components Structure
```
App (Main)
├── Navigation (Page switcher)
├── Database Page
│   ├── FileUpload (Drag & drop JSON upload)
│   └── DataPreview (Table with Hebrew headers)
└── Dashboard Page
    ├── KPI Cards (8 financial metrics)
    ├── Top Debtors List
    └── Charts (Bar, Pie, Horizontal bar)
```

## Data Structure

The application expects JSON data with these Hebrew field names:
- `חשבון` - Account number
- `תאור חשבון` - Account description  
- `סה'כ` - Total debt amount
- `חוב עתידי` - Future debt
- `>90` - Overdue debt over 90 days
- `61-90` - Debt 61-90 days old
- `31-60` - Debt 31-60 days old
- `1-30` - Debt 1-30 days old

## Key Calculations

### KPI Calculations (in `calculate_kpis` function)
- **Total Debt**: Sum of all `סה'כ` values
- **Future Debt**: Sum of all `חוב עתידי` values  
- **Overdue Debt**: Sum of all `>90` values
- **Average Aging Days**: Weighted average using midpoint of each aging category (15, 45, 75, 105 days)
- **Customer Count**: Number of customers with `סה'כ` > 0
- **Aging Categories**: Individual sums for each time period

## Testing

### Test Commands
```bash
# Run calculation tests
node test_calculations.js

# Serve locally for testing
python -m http.server 8000
# or
npx live-server
```

### Test Validation
- `test_calculations.js` contains comprehensive KPI calculation tests
- Tests validate against `sample-data.json` 
- Manual verification included for all calculations
- All tests must pass before deployment

## Development Guidelines

### RTL (Right-to-Left) Support
- All text content is in Hebrew
- Uses Heebo font from Google Fonts
- CSS includes RTL-specific styles and number formatting
- Charts configured for Hebrew labels and RTL layout

### State Management
- Uses React hooks: `useState`, `useEffect`, `useMemo`
- Data persisted in localStorage as JSON
- No external state management library

### Styling Approach
- Tailwind CSS with custom RTL configuration
- Embedded styles for chart containers and Hebrew typography
- Gradient backgrounds for KPI cards with hover effects
- Responsive design for mobile/tablet

## Common Tasks

### Adding New KPIs
1. Update `calculate_kpis` function in `index.html:122`
2. Add new KPICard component in dashboard section
3. Update test expectations in `test_calculations.js`

### Modifying Charts
- Chart configurations located in component functions: `AgingDistributionChart`, `AgingBreakdownChart`, `TopDebtorsChart`
- All charts use Chart.js with Hebrew labels
- Charts automatically destroy/recreate on data updates

### Data Validation
- JSON validation happens in `handle_file_upload` function
- Required fields checked against Hebrew field names
- Error messages displayed in Hebrew

## File Organization

```
customer-aging-dashboard/
├── index.html              # Complete application
├── sample-data.json         # Test data (Hebrew customer records)
├── test_calculations.js     # Calculation validation tests
├── proj.md                  # Project tracking and todos
├── README.md               # Deployment documentation
└── CLAUDE.md               # This file
```

## Deployment

### GitHub Pages
- No build process required
- Direct deployment of `index.html`
- All dependencies loaded from CDN
- Instructions in `README.md`

### Browser Requirements
- Modern browsers with ES6+ support
- Chart.js and React 18 compatibility
- Hebrew font rendering support

## Important Notes

- **Single File**: Everything is contained in `index.html` - avoid splitting into multiple files
- **Hebrew Language**: All UI text, field names, and data are in Hebrew
- **No Backend**: Fully client-side application with no server dependencies
- **CDN Dependencies**: React, Chart.js, Tailwind CSS all loaded from CDN
- **Test First**: Always run `test_calculations.js` before making calculation changes