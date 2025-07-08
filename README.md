# Customer Aging Dashboard - לוח בקרה דוחות גיל חוב

## Project Overview
A Hebrew-language customer aging dashboard for debt collection management, built with React, Tailwind CSS, and Chart.js as a single HTML file application.

## Features

### Database Page
- JSON file upload with drag & drop support
- Data validation for required Hebrew fields
- Preview table with Hebrew headers
- Data persistence using localStorage

### Dashboard Page
- **8 KPI Cards**:
  - סה"כ חוב בש"ח (Total Debt)
  - חוב עתידי (Future Debt)
  - חוב פג תוקף (Overdue Debt >90 days)
  - ממוצע ימי חוב (Average Aging Days)
  - מספר לקוחות (Customer Count)
  - חוב 1-30 יום (1-30 Days)
  - חוב 31-60 יום (31-60 Days)
  - חוב 61-90 יום (61-90 Days)

- **Charts & Visualizations**:
  - Aging Distribution Bar Chart
  - Aging Breakdown Pie Chart
  - Top 5 Debtors Horizontal Bar Chart
  - Top Debtors List

## Technical Stack
- React 18 (via CDN)
- Tailwind CSS
- Chart.js
- Hebrew fonts (Heebo)
- Single HTML file architecture
- RTL (Right-to-Left) layout support

## JSON Data Format
The application expects JSON data with the following Hebrew field names:

```json
[
  {
    "חשבון": "account_number",
    "תאור חשבון": "account_description",
    "מטבע החשבון": "ש\"ח",
    "סה'כ": "total_amount",
    "יתרה בשקל": "balance_in_shekels",
    "חוב עתידי": "future_debt",
    ">90": "overdue_over_90_days",
    "61-90": "overdue_61_90_days",
    "31-60": "overdue_31_60_days",
    "1-30": "overdue_1_30_days"
  }
]
```

## Local Development

1. **Clone/Download** the project files
2. **Open** `index.html` in a web browser
3. **Upload** a JSON file using the sample format
4. **Navigate** to the dashboard to view analytics

### Using a Local Server (Recommended)
```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000

# Node.js (if you have live-server installed)
npx live-server

# Then open http://localhost:8000
```

## GitHub Pages Deployment

### Option 1: Direct Upload
1. Create a new GitHub repository
2. Upload all files to the repository
3. Go to Settings > Pages
4. Select source: Deploy from a branch
5. Choose branch: main
6. Your dashboard will be available at: `https://username.github.io/repository-name`

### Option 2: GitHub Actions (Recommended)
1. Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    
    - name: Deploy to GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./
```

2. Push to main branch
3. GitHub will automatically deploy your site

## File Structure
```
customer-aging-dashboard/
├── index.html              # Main application (single file)
├── sample-data.json         # Sample data for testing
├── test_calculations.js     # Test validation script
├── proj.md                  # Project tracking
└── README.md               # This file
```

## Browser Compatibility
- Chrome 60+
- Firefox 60+
- Safari 12+
- Edge 79+

## RTL Support
The application is fully optimized for Hebrew (RTL) layout:
- Hebrew typography using Heebo font
- Right-to-left text alignment
- Proper number formatting for Hebrew locale
- RTL-aware chart layouts

## Sample Data
Use the provided `sample-data.json` file to test the application functionality. The file contains realistic customer aging data with various debt categories.

## Calculated KPIs
- **Total Debt**: Sum of all customer debt amounts
- **Future Debt**: Sum of all future-dated debts
- **Overdue Debt**: Sum of debts over 90 days old
- **Average Aging Days**: Weighted average of debt aging periods
- **Customer Count**: Number of customers with outstanding debt
- **Aging Categories**: Breakdown by 1-30, 31-60, 61-90 day periods

## Troubleshooting

### Data Not Loading
- Ensure JSON file has all required Hebrew field names
- Check browser console for JavaScript errors
- Verify JSON syntax is valid

### Charts Not Displaying
- Make sure Chart.js loads properly (check network tab)
- Ensure data contains numeric values
- Check browser compatibility

### Hebrew Text Issues
- Verify Heebo font loads from Google Fonts
- Check that `dir="rtl"` is set on HTML element
- Ensure browser supports Hebrew text rendering

## Development Notes
- All calculations are performed client-side
- Data is stored in browser localStorage
- No server-side dependencies required
- Fully responsive design for mobile/tablet
- Accessible design following WCAG guidelines