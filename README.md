# Satellite Tracker Analysis - Interactive Orbital Mechanics Visualisation

## A Python Flask-based web application for real-time satellite orbital calculations and 3D trajectory visualisation using SGP4 propagation

---

## Overview

Satellite Tracker Analysis is a comprehensive web application that combines the power of Python's orbital mechanics libraries with an interactive browser-based interface. This tool enables users to visualise satellite trajectories in real-time, analyze altitude profiles over time, and experiment with Keplerian orbital elements to understand satellite motion.

The application leverages the SGP4 (Simplified General Perturbations) propagation algorithm to accurately calculate satellite positions from Two-Line Element (TLE) data. This is the same standardized format used by NORAD and space agencies worldwide. Whether you are a satellite operator, aerospace student, amateur astronomer, or space enthusiast, this tool provides an intuitive way to explore orbital mechanics without complex software installations.

### Key Features

- Real-time altitude vs. time graphing with 24-hour propagation
- Interactive 3D orbital trajectory visualisation with Earth reference
- TLE data parsing and automatic Keplerian element extraction
- Manual control over six orbital parameters via intuitive sliders
- CSV data export functionality for further analysis
- Responsive design that works on desktop and mobile devices
- Dark space-themed interface with smooth animations

---

## Application Screenshots

### Main Interface
![Main Dashboard](screenshots/dashboard.png)
*The main interface showing altitude graph, 3D orbit visualisation, and control panel*

### Altitude vs Time Graph
![Altitude Graph](screenshots/altitude-graph.png)
*24-hour altitude profile calculated using SGP4 propagation from TLE data*

### 3D Orbital Visualisation
![3D Orbit](screenshots/3d-orbit.png)
*Interactive 3D view showing satellite trajectory, Earth position, and periapsis marker*

### Control Panel
![Control Panel](screenshots/controls.png)
*TLE input section and Keplerian element sliders for real-time orbit manipulation*

---

## Installation Instructions

### Prerequisites

Before installing, ensure you have the following installed on your system:
- Python 3.7 or higher
- pip (Python package manager)

### Step 1: Download the Code

Save the provided code as `app.py` in your desired project directory.

### Step 2: Install Required Python Packages

Open a terminal or command prompt, navigate to your project directory, and run:
```bash
pip install flask numpy sgp4
```

This will install:

Flask: Web framework for the application server
NumPy: Numerical computing library for calculations
sgp4: SGP4 satellite propagation library

Step 3: Verify Installation
You can verify the packages are installed correctly by running:
```bash
python -c "import flask, numpy, sgp4; print('All packages installed successfully')"
```

## Usage Instructions

### Starting the Application

1. Open a terminal or command prompt
2. Navigate to the directory containing app.py
3. Run the following command:
```bash
python app.py
```
4. You should see output similar to:
```bash
============================================================
SATELLITE TRACKER ANALYSIS - Flask Server
============================================================
✓ Original Python code integrated (SGP4 calculations)
✓ Server starting on: http://localhost:5001
✓ Press Ctrl+C to stop the server
============================================================
```
5. Open your web browser and navigate to http://localhost:5001

## Using the Application

### Loading TLE Data

The application comes pre-loaded with TLE data for the International Space Station (ISS). To use different satellite data:

1. Obtain TLE data from sources like:

CelesTrak
Space-Track.org
N2YO.com


2. Paste the two TLE lines into the input fields in the right panel
3. Click "Load from TLE" to automatically extract orbital parameters
4. The visualiation will update automatically

### Example TLE format:

```bash
1 25544U 98067A   21257.91276829  .00000825  00000-0  24323-4 0  9991
2 25544  51.6461  89.6503 0003031 120.4862 259.0942 15.48881082307119
```

Adjusting Orbital Parameters
Use the interactive sliders to manually adjust Keplerian elements:

| Parameter           | Range         | Description                                                            |
|---------------------|---------------|------------------------------------------------------------------------|
| Semi-Major Axis     | 2000-50000 km | Controls orbit size                                                    |
| Eccentricity        | 0-0.99        | Controls orbit shape (0 = circular; approaching 1 = highly elliptical) |
| Inclination         | 0-180°        | Angle of orbit relative to equator                                     |
| RAAN                | 0-360°        | Right Ascension of Ascending Node Orientation of orbit plane           |
| Argument of Perigee | 0-360°        | Rotation of orbit within its plane                                     |
| Mean Anomaly        | 0-360°        | Satellite position along its orbit                                     |                      |   |


After adjusting parameters, click "Update Visualisation" to recalculate and display the new orbit.

## Understanding the Visualisations

### Altitude Graph:

- X-axis: Time in hours (0-24 hour period)
- Y-axis: Altitude above Earth's surface in kilometers
- Shows how satellite altitude varies over one complete day

### 3D Orbit Plot:

- Blue line: Complete orbital trajectory
- Green sphere: Earth center position
- Red marker: Periapsis (closest point to Earth)
- Interactive: Click and drag to rotate, scroll to zoom

### Exporting Data
Click the "Download CSV" button to export the current altitude data as a CSV file. The file includes:

- Export timestamp
- Time values in hours
- Corresponding altitude values in kilometers

The CSV file can be opened in Excel, Google Sheets, or any data analysis software.
Stopping the Application

To stop the server:

- Press Ctrl+C in the terminal where the application is running
- Wait for the shutdown message to appear


## Technical Details

### Backend Calculations

The application performs two main types of calculations:

1. SGP4 Propagation: Uses TLE data to calculate precise satellite positions at 1-minute intervals over 24 hours

2. Keplerian Orbit Generation: Computes 3D orbital paths from classical orbital elements using coordinate transformations

### Default Values

When the application starts, it uses these default Keplerian elements:

| Element             | Default Value |
|---------------------|---------------|
| Semi-Major Axis     | 10000 km      |
| Eccentricity        | 0.1           |
| Inclination         | 90°           |
| RAAN                | 40°           |
| Argument of Perigee | 1°            |
| Mean Anomaly        | 1°            |

### Port Configuration

The application automatically finds an available port between 5001 and 5099. If port 5001 is in use, it will try subsequent ports until it finds one that is free.

### Browser Compatibility

The application works best on modern browsers:

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

### API Endpoints

| Method | Endpoint       | Description                                                                 |
|--------|----------------|-----------------------------------------------------------------------------|
| GET    | /              | Main application interface                                                  |
| POST   | /api/calculate | Backend calculation endpoint (accepts JSON with TLE and orbital parameters) |

## Troubleshooting

### Common Issues
#### Issue: Port already in use

Solution: The application will automatically try alternate ports. Check the terminal output for the actual port being used.

#### Issue: Module not found error

Solution: Ensure all required packages are installed using ```bash pip install flask numpy sgp4 ```

#### Issue: TLE parsing error

Solution: Verify that your TLE data is correctly formatted with exactly 69 characters per line and proper spacing

#### Issue: Visualisation not updating

Solution: Check browser console for JavaScript errors. Ensure you have a stable internet connection for loading Plotly library from CDN.

#### Issue: Empty or incorrect plots

Solution: Verify that orbital parameters are within valid ranges. Extreme values may cause calculation errors.

## File Structure

```bash
project-directory/
│
├── app.py                 # Main Flask application file
├── README.md             # This file
└── screenshots/          # (Optional) Directory for documentation images
    ├── dashboard.png
    ├── altitude-graph.png
    ├── 3d-orbit.png
    └── controls.png
```

## Project Architecture

### Frontend Components

- HTML Template: Single-page application embedded within Flask
- CSS Styling: Custom dark theme with gradient effects and glassmorphism
- JavaScript: Handles user interactions, API calls, and Plotly visualisations
- Plotly.js: Library for interactive 2D and 3D plotting

### Backend Components

- Flask Routes: Serves HTML and handles API requests
- SGP4 Module: Performs satellite propagation calculations
- NumPy: Handles numerical computations and array operations
- Orbital Mechanics Functions: Custom implementations for Keplerian element calculations

## Understanding Orbital Mechanics

### Two-Line Element (TLE) Format

TLE data is a standardized format for describing satellite orbits. Each satellite has two lines of data:

- Line 1: Contains satellite catalog number, epoch time, and drag terms
- Line 2: Contains orbital elements (inclination, RAAN, eccentricity, etc.)

### Keplerian Elements Explained

The six classical orbital elements define a satellite's orbit:

1. Semi-Major Axis (a): Half the longest diameter of the orbital ellipse. Determines orbital period.
2. Eccentricity (e): Shape of the orbit. 0 is circular, values approaching 1 are highly elliptical.
3. Inclination (i): Tilt of orbital plane relative to Earth's equator. 0° is equatorial, 90° is polar.
4. Right Ascension of Ascending Node (RAAN/Ω): Orientation of the orbital plane in space.
5. Argument of Perigee (ω): Orientation of the ellipse within the orbital plane.
6. Mean Anomaly (M): Position of satellite along its orbit at epoch time.

### SGP4 Propagation

SGP4 is a mathematical model that predicts satellite positions by accounting for:

- Earth's gravitational field irregularities
- Atmospheric drag effects
- Solar and lunar gravitational perturbations
- Solar radiation pressure

## Educational Use Cases

This application is ideal for:

- Aerospace Engineering Students: Visualising theoretical orbital mechanics concepts
- Amateur Radio Operators: Tracking satellite passes for communication
- Astronomy Enthusiasts: Following satellite positions and predicting visibility
- Educators: Demonstrating orbital dynamics in interactive lessons
- Research: Analysing orbital decay, station-keeping requirements, or mission planning

## Performance Notes:

- Calculation Time: Typically 1-3 seconds for 24-hour propagation with 1-minute resolution
- Memory Usage: Approximately 50-100 MB for typical operations
- Browser Performance: 3D visualization performs best with hardware acceleration enabled

## Data Sources

Recommended sources for TLE Data:

| Source          | Description                                                  |
|-----------------|--------------------------------------------------------------|
| CelesTrak       | Comprehensive catalog of active satellites; updated daily    |
| Space-Track.org | Official US Space Force catalog (requires free registration) |
| N2YO.com        | User-friendly interface with real-time tracking              |
| Heavens-Above   | Amateur astronomy focused with visibility predictions        |

## Future Enhancements

Potential features for future versions:

- Ground track visualization on 2D world map
- Real-time satellite position updates
- Multiple satellite comparison
- Orbital maneuver planning tools
- Historical orbit analysis
- Ground station visibility calculations
- Integration with satellite databases for automatic TLE updates

## Mathematical References

The orbital calculations are based on:

- Vallado, D. A., "Fundamentals of Astrodynamics and Applications"
- Hoots, F. R., Roehrich, R. L., "Spacetrack Report No. 3: Models for Propagation of NORAD Element Sets"
- Curtis, H. D., "Orbital Mechanics for Engineering Students"

## License and Credits

This application uses the following open-source libraries:

| Library   | License              |
|-----------|----------------------|
| Flask     | BSD-3-Clause License |
| NumPy     | BSD License          |
| sgp4      | MIT License          |
| Plotly.js | MIT License          |

## Support and Contributions

For issues, questions, or suggestions:

1. Check the troubleshooting section above
2. Verify your Python and package versions meet requirements
3. Ensure TLE data is correctly formatted
4. Check browser console for JavaScript errors

## Version History

v1.0: Initial release with SGP4 propagation, 3D visualisation, and TLE parsing

## System Requirements

### Minimum Requirements

- Python 3.7+
- 2 GB RAM
- Modern web browser with JavaScript enabled
- Internet connection for CDN resources (Plotly.js)

### Recommended

- Python 3.9+
- 4 GB RAM
- Chrome or Firefox latest version
- Dedicated GPU for smooth 3D rendering

## Quick Start Example

For a quick test run with ISS data:
```bash
# Install dependencies
pip install flask numpy sgp4

# Run application
python app.py

# Open browser to http://localhost:5001
```

Then:

1. Click "Update Visualisation" to see ISS orbit
2. Experiment with sliders to modify orbital parameters
3. Click "Download CSV" to export data

## Acknowledgments

This application implements orbital mechanics algorithms based on decades of research in astrodynamics and space operations. Special recognition to the developers of the SGP4 library and the maintainers of public TLE data sources that make projects like this possible.

### Made with Python, Flask, and a passion for Space Exploration