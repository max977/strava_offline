# Strava Offline Dashboard

A powerful, self-contained web application for analyzing your Strava activities offline. Upload your activity data and GPX route files to visualize performance metrics, track personal bests, and explore your activity routes on an interactive map.

## Features

✨ **Core Features**
- 📊 Real-time activity analysis and statistics
- 🗺️ Interactive route visualization with OpenStreetMap integration
- 🏃 Support for multiple activity types (Runs, Rides, Swims)
- 🎯 Personal best tracking (fastest speed, longest distance per activity type)
- 📈 Monthly and yearly performance analytics with interactive charts

🔧 **Advanced Features**
- 📅 Flexible filtering by date range, activity type, and duration
- 📊 Interactive charts with hover tooltips (Distance, Activities, Type Distribution, Speed)
- 🖱️ Click on monthly/yearly charts to filter entire dashboard in real-time
- 🎨 Beautiful, responsive UI with dark/light mode support
- 🔐 100% offline - no data leaves your device
- ⚡ Fast performance with GPX.GZ decompression support

## Getting Started

### Prerequisites

No installation required! This is a single-file HTML application that runs entirely in your web browser.

**Requirements:**
- Modern web browser (Chrome, Firefox, Safari, Edge)
- Your Strava data export files (CSV + GPX folder)

### How to Run

1. **Download the Dashboard**
   ```bash
   # Clone or download the repository
   git clone https://github.com/max977/strava_offline.git
   cd strava_offline
   ```

2. **Open in Browser**
   - Double-click `strava_offline.html` to open it directly in your browser, OR
   - Serve it locally using Python:
     ```bash
     # Python 3
     python -m http.server 8000
     # Then visit http://localhost:8000
     ```

3. **Export Your Strava Data**
   - Go to [Strava Settings → Data](https://www.strava.com/settings/profile)
   - Click "Get Your Strava Data"
   - Download your export (includes `activities.csv` and `activities/` folder with GPX files)

## How to Use

### Step 1: Load Your Data

1. Open the dashboard in your browser
2. Click **"Activities CSV"** button and select your `activities.csv` file
3. Click **"GPX Folder"** button and select the `activities` folder containing your route files
4. Click **"Load & Analyze"** button
5. Wait for processing (displays route count and any skipped .fit.gz files)

**Note:** The dashboard supports `.gpx` and `.gpx.gz` files. Binary `.fit.gz` files require conversion to GPX format first (use tools like [FIT to GPX converter](https://www.gpsvisualizer.com/convert_input)).

### Step 2: Explore Your Activities

#### View Recent Activities
- Browse your activities in the **"Recent Activities"** section
- Activities are sorted by date (newest first)
- Each activity shows: name, date, distance, duration, and average speed
- Click any activity to display its route on the map

#### View Route on Map
- The interactive map displays your activity routes
- Different colors for different activity types:
  - 🔴 **Red** = Running
  - 🟠 **Orange** = Cycling
  - 🔵 **Blue** = Swimming
- Click an activity to center and zoom to its route

#### Check Personal Bests
- **Personal Bests** section shows:
  - Fastest speed for each activity type
  - Longest distance for each activity type
- Click any personal best card to jump to that activity on the map
- Cards highlight on hover showing they're clickable

### Step 3: Analyze Performance with Filters

#### Basic Filters
- **Activity Type:** Filter to Runs, Rides, or Swims
- **From Date:** Set start date (all before this date excluded)
- **To Date:** Set end date (all after this date excluded)
- **Min Duration:** Filter activities shorter than specified duration

All filters update in real-time - statistics, activities list, and charts refresh instantly.

### Step 4: View Performance Analytics

#### Monthly Performance Charts
- **Monthly Distance:** Bar chart showing total distance per month
- **Monthly Activities:** Line chart showing activity count trends
- **Activity Type Distribution:** Doughnut chart showing run/ride/swim breakdown
- **Monthly Average Speed:** Radar chart showing speed variations

**Interactive Feature:** Click any bar or point on the first three monthly charts to filter the entire dashboard to just that month. A blue border highlights the selected month.

#### Yearly Performance Charts
- **Yearly Distance:** Total distance per year
- **Yearly Activities:** Activity count per year
- **Yearly Type Breakdown:** Stacked bar chart comparing activity types across years
- **Yearly Average Speed:** Speed trends across years

**Interactive Feature:** Click any bar or point on the first three yearly charts to filter to just that year.

#### Overview Statistics
- **Total Activities:** Number of activities in current filter
- **Total Distance:** Combined distance of all activities
- **Total Time:** Combined duration of all activities
- Activity-specific cards showing counts and distances per type

### Step 5: Export-Ready Data

All data is calculated from your filtered activities:
- Statistics update when filters change
- Charts reflect filtered data in real-time
- Personal bests recalculate based on current filters
- No data is stored or transmitted

## File Format Requirements

### Activities CSV
Expected columns (from Strava export):
```
Activity Date, Activity Type, Activity Name, Distance, Elapsed Time, Moving Time, Filename
```

**Example:**
```
2025-01-15, Run, Morning 5K, 5042, 1847, 1800, activities/14380243710.gpx.gz
2025-01-14, Ride, Evening Commute, 12500, 2400, 2350, activities/14380243711.gpx.gz
```

### GPX Files
Supported formats:
- `.gpx` - Standard uncompressed GPX files
- `.gpx.gz` - Gzip-compressed GPX files (automatically decompressed)
- `.fit.gz` - Garmin binary format (not supported, requires conversion)

The dashboard automatically decompresses `.gpx.gz` files during loading.

## Tips & Tricks

### Optimize Performance
- For large datasets (1000+ activities), filtering by date range first speeds up analysis
- Charts are cached and only rebuild when filters change

### Analyze Trends
1. Click on monthly charts to focus on specific months
2. Compare monthly patterns across years using yearly charts
3. Use the type filter to analyze one activity type separately

### Find Specific Activities
1. Use date filters to narrow down the time period
2. Filter by activity type (Run, Ride, or Swim)
3. Use duration filter to find longer/shorter activities
4. Scroll through the activities list or click to view on map

### Troubleshooting

**"Route data not available"**
- The GPX file might not have been selected
- File might be corrupted or in wrong format
- Try re-selecting the GPX folder

**Charts not updating**
- Try refreshing the page and reloading data
- Check browser console for errors (F12)

**Slow performance**
- Close other browser tabs
- Try with a smaller date range first
- Check your internet (map tiles are loaded online)

**Missing routes on map**
- Ensure you selected the activities folder containing GPX files
- Some GPX files may be corrupted (dashboard skips these)
- Check the loaded routes count in the toast message

## Browser Compatibility

✅ **Fully Supported**
- Chrome/Chromium (88+)
- Firefox (87+)
- Safari (14+)
- Edge (88+)

⚠️ **Requires Modern Browser Features**
- ES6 JavaScript support
- File API access
- LocalStorage (optional, not required)
- Geolocation (optional, only for map centering)

## Technical Details

### Architecture
- **Single-file HTML application** - No build process or dependencies
- **External libraries:** Leaflet (mapping), Chart.js (analytics), Pako (GZ decompression)
- **Data processing:** All calculations happen in-browser
- **Storage:** No persistent storage (data cleared on page refresh)

### Performance
- CSV parsing: Custom parser handles quoted values
- GPX parsing: DOM-based XML parser
- Chart rendering: Chart.js with responsive design
- Map rendering: Leaflet with OpenStreetMap tiles

### Data Privacy
- **100% Offline:** No server communication
- **No tracking:** No analytics or telemetry
- **Local processing:** All calculations on your device
- **No storage:** Data is cleared when you close the browser

## Keyboard Shortcuts

- `F12` - Open developer console (for debugging)
- `Ctrl+A` (or `Cmd+A` on Mac) - Select all text

## Known Limitations

1. **No export functionality** - Data is for viewing only (screenshots or browser tools can capture)
2. **No persistent storage** - Data resets on page refresh
3. **Map tiles require internet** - Route display needs OpenStreetMap connection
4. **.fit.gz not supported** - Must convert Garmin FIT files to GPX first
5. **CSV must be from Strava** - Custom CSVs require the correct column names

## Contributing

Found a bug or have a feature request? 

1. Check existing [GitHub Issues](https://github.com/yourusername/strava-offline-dashboard/issues)
2. Create a new issue with:
   - Description of the problem
   - Steps to reproduce
   - Browser and OS version
   - Screenshot if relevant

## Future Enhancements

🚀 Potential features for future versions:
- Export filtered data as CSV
- Segment analysis and comparisons
- Elevation profile graphs
- Monthly goal tracking
- Custom color themes
- Multi-language support
- PWA offline support

## License

MIT License - Feel free to use, modify, and distribute

## Credits

**Built with:**
- [Leaflet](https://leafletjs.com/) - Interactive mapping
- [Chart.js](https://www.chartjs.org/) - Data visualization
- [Pako](https://github.com/nodeca/pako) - GZ decompression
- [FontAwesome](https://fontawesome.com/) - Icons
- [OpenStreetMap](https://www.openstreetmap.org/) - Map tiles

## Support

For issues, questions, or suggestions:
1. Check this README thoroughly
2. Search existing GitHub issues
3. Create a new issue with detailed information
4. Include browser console errors (F12 → Console tab)

---

**Happy analyzing! 🏃🚴🏊**

Built with ❤️ for the fitness tracking community
