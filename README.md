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

-
    ```
    pip install numpy matplotlib
    pip install scikit-learn
    ```


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

### AI-Assisted Drone Conflict Detection Workflow
- `Model Training`:
    - Trains a Random Forest classifier on example data (`X_train`, `y_train`)
    - Uses simple features (e.g., minimum time and spatial differences) to distinguish between conflicting and non-conflicting drone pairs
- `Feature Extraction`:
    - The extract_features function computes basic features from each drone pair
    - Placeholders are used in the example; should be replaced with actual calculations relevant to your data
- `Pre-Filtering`:
    - `ai_prefilter_deconfliction` function streamlines conflict checks
    -  Extracts features for each drone pair
    -  Uses the AI model to predict if a conflict is likely
    -  Runs the detailed check_conflict function only for pairs flagged as likely conflict
    -  Collects and returns the actual conflicts 

### Core Services

- `DeconflictionService`:  
    - Registers flights and checks for conflicts  
    - Initializes with safety parameters (minimum safe distance and time threshold)  
    - Interpolates drone trajectories for precise, time-stamped conflict checking  
    - Handles edge cases (single drone, no overlap, spatial/temporal overlap, etc.)  
    - Returns `"conflict detected"` with details or `"clear"` if safe

- `Check Mission Safety`:  
    - Simple interface function for conflict detection  
    - Sets up `DeconflictionService` with safety parameters  
    - Registers all other drone flights  
    - Checks if the new mission’s path and timing overlap dangerously with any existing flights  
    - Returns mission status and any detected conflicts

- `DeconflictionVisualizer`:  
    - Creates static and animated visualizations  
    - Provides 3D/2D plots of drone missions  
    - Animates drone movements and highlights conflicts  
    - Offers an interactive slider to explore drone positions over time  
    - Clearly marks conflict points and provides visual/text alerts


## Custom Usage

To check your own drone missions:

### 1. Create waypoints for each drone's path:
 
    ```
    waypoints = [
        Waypoint(0, 0, 0),
        Waypoint(50, 50, 10),
        Waypoint(100, 0, 20)
    ]
    ```

### 2. Define flight plans with time windows

 
    ```
    from datetime import datetime, timedelta

    now = datetime.now()
    flight_plan = DroneFlightPlan(
        drone_id="drone1",
        waypoints=waypoints,
        start_time=now,
        end_time=now + timedelta(minutes=10)
    )
    ```
    
### 3. AI-Assisted Deconfliction

 
    ```
    model = RandomForestClassifier(n_estimators=10, random_state=42)
    model.fit(X_train, y_train)


    def extract_features(pair):
        min_time_diff = 2  # placeholder
        min_spatial_dist = 7  # placeholder
        return np.array([[min_time_diff, min_spatial_dist]])


    def ai_prefilter_deconfliction(pairs):
    conflicts = []
    for pair in pairs:
        features = extract_features(pair)
        prediction = model.predict(features)
        if prediction == 1:  # likely conflict
            if check_conflict(pair):  # original detailed check
                conflicts.append(pair)
    return conflicts
    ```


### 3. Check for conflicts between missions:
 
    ```
    result = check_mission_safety(primary_mission, [other_flight1, other_flight2])
    print(f"Mission status: {result.status}")
    ```


### 4. Visualize the results:

    ```
    visualizer = DeconflictionVisualizer()
    fig = visualizer.visualize_mission(
        primary_mission,
        [other_flight1, other_flight2],
        result.conflicts
    )
    plt.show()
    ```


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
