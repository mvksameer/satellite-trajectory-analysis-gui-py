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



After adjusting parameters, click "Update Visualization" to recalculate and display the new orbit.
Understanding the Visualizations
Altitude Graph:

X-axis: Time in hours (0-24 hour period)
Y-axis: Altitude above Earth's surface in kilometers
Shows how satellite altitude varies over one complete day

3D Orbit Plot:

Blue line: Complete orbital trajectory
Green sphere: Earth center position
Red marker: Periapsis (closest point to Earth)
Interactive: Click and drag to rotate, scroll to zoom

Exporting Data
Click the "Download CSV" button to export the current altitude data as a CSV file. The file includes:

Export timestamp
Time values in hours
Corresponding altitude values in kilometers

The CSV file can be opened in Excel, Google Sheets, or any data analysis software.
Stopping the Application
To stop the server:

Press Ctrl+C in the terminal where the application is running
Wait for the shutdown message to appear


Technical Details
Backend Calculations
The application performs two main types of calculations:

SGP4 Propagation: Uses TLE data to calculate precise satellite positions at 1-minute intervals over 24 hours
Keplerian Orbit Generation: Computes 3D orbital paths from classical orbital elements using coordinate transformations

Default Values
When the application starts, it uses these default Keplerian elements:
ElementDefault ValueSemi-Major Axis10000 kmEccentricity0.1Inclination90°RAAN40°Argument of Perigee1°Mean Anomaly1°
Port Configuration
The application automatically finds an available port between 5001 and 5099. If port 5001 is in use, it will try subsequent ports until it finds one that is free.
Browser Compatibility
The application works best on modern browsers:

Chrome 90+
Firefox 88+
Safari 14+
Edge 90+