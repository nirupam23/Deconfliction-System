# Drone Mission Deconfliction System

## Overview

The Drone Mission Deconfliction System is a comprehensive solution for detecting and visualizing potential conflicts between multiple drone flight paths in 3D space and time. This system helps ensure safe drone operations by identifying when and where drones might come too close to each other during their missions.

## Key Features

- Spatiotemporal conflict detection between multiple drone flight plans
- 3D visualization of drone trajectories and conflict points
- Time-based animations showing drone movements and potential conflicts
- Interactive 4D visualization with time slider for detailed analysis
- Configurable safety parameters (minimum safe distance and time threshold)

## Setup Instructions

### Prerequisites

- Python 3.8 or higher
- Jupyter Notebook or JupyterLab

### Required Packages

Install the following Python packages:
-'pip install numpy matplotlib'


### Download the Notebook

- Download the `Deconflication.ipynb` file to your local machine

## Execution Instructions

### Open the Notebook

- Launch Jupyter Notebook or JupyterLab
- Navigate to and open the `Deconflication.ipynb` file

### Run the Cells

- Execute all cells in order from top to bottom
- This will load all necessary classes and functions

### Run the Example Scenarios

- The notebook includes a `run_example()` function that demonstrates the system
- It will run two scenarios: one with conflicts and one without
- Results will be displayed in the notebook and saved as image/video files

### Examine the Output

- Console output will show detected conflicts with details
- Static visualizations will be saved as PNG files
- Animations will be saved as MP4 files (requires ffmpeg)
- Interactive 4D visualizations can be explored within the notebook

## System Components

### Data Structures

- `Waypoint`: Represents a 3D point in space (x, y, z)
- `DroneFlightPlan`: Contains drone ID, waypoints, and time window
- `Conflict`: Details about a detected conflict (location, time, distance)
- `ConflictResult`: Overall result of a safety check

### Core Services

- `DeconflictionService`: Registers flights and checks for conflicts
- `check_mission_safety()`: Simple interface function for conflict detection
- `DeconflictionVisualizer`: Creates static and animated visualizations

## Custom Usage

To check your own drone missions:

### 1. Create waypoints for each drone's path:
- 
    ```
    waypoints = [
        Waypoint(0, 0, 0),
        Waypoint(50, 50, 10),
        Waypoint(100, 0, 20)
    ]
    ```

### 2. Define flight plans with time windows:
-
    '''

    from datetime import datetime, timedelta

    now = datetime.now()
    flight_plan = DroneFlightPlan(
    drone_id="drone1",
    waypoints=waypoints,
    start_time=now,
    end_time=now + timedelta(minutes=10)
    )
    '''


### 3. Check for conflicts between missions:
result = check_mission_safety(primary_mission, [other_flight1, other_flight2])
print(f"Mission status: {result.status}")

text

### 4. Visualize the results:
visualizer = DeconflictionVisualizer()
fig = visualizer.visualize_mission(
primary_mission,
[other_flight1, other_flight2],
result.conflicts
)
plt.show()

text

## Configuration Options

- Adjust safety parameters in the `check_mission_safety()` function:
    - `safety_buffer`: Minimum safe distance between drones in meters (default: 10.0)
    - `time_threshold`: Time window for conflict detection in seconds (default: 5.0)

- Visualization options:
    - `is_3d`: Set to True for 3D visualizations, False for 2D (default: True)
    - `fps` and `duration`: Control animation speed and length

## Example Output

When running the example scenarios, you'll see:

- Conflict detection results in the console
- Static visualizations of flight paths with conflict points highlighted
- Animations showing drone movements over time
- Interactive 4D visualizations with time slider control
