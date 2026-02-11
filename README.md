# 🚲 Bike Checker

A minimalist iOS-style web app for checking bike availability at London cycle hire stations. Built as a personal tool for the developer.

## ⚠️ Important Note

**This app is customized specifically for my personal use** with hardcoded stations. If you want to use this code, you'll need to customize it for your own locations and bike share system.

## Features

- **Weather Widget**: Real-time weather display with temperature, conditions, and wind information
- **Location Checker**: Quick view of bike/dock availability at favorite locations (home, work, etc.)
- **Route Planner**: Check availability at both pickup and dropoff stations for planned routes
- **Backup Stations**: Automatically shows nearby alternative stations when availability is low
- **iOS-Style UI**: Native app feel with dark mode and iOS design patterns
- **PWA Support**: Installable as a standalone app on iOS/Android

## Screenshots

The app features:
- Clean, card-based interface
- Real-time station data with color-coded availability (green/yellow/red)
- Simple route planning with start/destination picker
- Weather integration
- Settings panel for TfL API key (app will still work without need for TfL API key, just may hit rate limits)

## How It Works

The app fetches real-time data from the Transport for London (TfL) BikePoint API and displays:
- 🚲 Regular bikes available
- ⚡ E-bikes available  
- 📍 Empty docks available

Availability is color-coded:
- 🟢 **Green**: Good availability
- 🟡 **Yellow**: Low availability
- 🔴 **Red**: Empty/unavailable

## Customization Required

To use this for yourself, you'll need to modify:

### 1. Station IDs
Update the `STATIONS` and `BACKUP` objects (around line 233-321) with your preferred stations:

```javascript
const STATIONS = {
  home: {
    label: 'Your Location Name',
    ids: {
      'BikePoints_123': 'Station Name 1',
      'BikePoints_456': 'Station Name 2'
      // Add your stations
    }
  },
  // ... add more locations
};
```

### 2. Find Station IDs
Get BikePoint IDs from the TfL API:
- API endpoint: `https://api.tfl.gov.uk/BikePoint`
- Find stations near your locations
- Note the `id` field (e.g., `BikePoints_123`)

### 3. Place Names & Icons
Update the `PLACE_NAMES` and `PLACE_ICONS` objects (around line 323-335) to match your locations.

### 4. Weather Location
Update the weather coordinates in `loadWeather()` (around line 471):

```javascript
async function loadWeather() {
  const url = `https://api.open-meteo.com/v1/forecast?latitude=YOUR_LAT&longitude=YOUR_LON...`;
  // ...
}
```

### 5. Thresholds (Optional)
Adjust availability thresholds in the `THRESHOLDS` object (around line 337):

```javascript
const THRESHOLDS = {
  bikes: 2,          // Warn when ≤2 bikes
  docks_arrive: 2,   // Warn when ≤2 docks
  location: 2        // General location threshold
};
```

## API Key Setup

The app uses the public TfL API. For better rate limits:

1. Get a free API key from [TfL API Portal](https://api-portal.tfl.gov.uk/)
2. In the app, tap ⚙️ Settings
3. Enter your API key
4. Tap Save

## Installation

### As a Web App
1. Open `index.html` in a web browser
2. Done! (works offline after first load)

### As a PWA (iOS)
1. Open in Safari
2. Tap the Share button
3. Tap "Add to Home Screen"
4. Launch from your home screen like a native app

## Tech Stack

- Vanilla JavaScript (no dependencies)
- TfL BikePoint API
- Open-Meteo Weather API
- LocalStorage for settings
- CSS Variables for theming
- Progressive Web App capabilities

## Browser Support

Optimized for:
- Safari (iOS/macOS)
- Chrome (Android/Desktop)
- Other modern browsers with CSS Grid and Custom Properties support

## License

This is a personal hobby project. Feel free to use the code however you like, but remember you'll need to customize it for your own use case.

## Contributing

This is primarily a personal project, but if you have suggestions or improvements, feel free to open an issue or PR!

---

**Note**: This app is not affiliated with Transport for London or Santander Cycles. It simply uses publicly available API data.
