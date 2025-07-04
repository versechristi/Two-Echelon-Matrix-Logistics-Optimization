# Logistics Optimization System

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

This is a comprehensive desktop application designed for the **Multi-Depot, Two-Echelon Vehicle Routing Problem with Drones and Split Deliveries (MD-2E-VRPSD)**. The system deeply integrates two modern logistics scenarios: **drone collaboration** and **split deliveries**, and presents them through a feature-rich Graphical User Interface (GUI). Users can easily configure problem parameters, select optimization algorithms, execute the optimization process, and perform multi-dimensional visual analysis of the results.

The core application scenario involves one or more central depots replenishing multiple sales outlets (first echelon of transport). Subsequently, these sales outlets act as secondary hubs, utilizing a fleet of **trucks and drones** to complete the "last-mile" delivery to end customers (second echelon of transport).

## System Interface & Core Functionality Demo

The system provides a highly integrated and user-friendly graphical interface, combining complex parameter configuration, algorithm execution, and results visualization into a single seamless experience.

![24c4676c66dd8844b5e4303636b804f4](https://github.com/user-attachments/assets/55a730e8-e97c-4479-b67b-2554c0584299)

* **Left Panel (Control Panel)**: Integrates parameter configuration sections (Data Generation, Vehicle/Drone Properties, Objective Function, Algorithm Parameters) and execution controls (Generate Data, Algorithm Selection, Run Optimization).
* **Right Panel (Results Display)**: Clearly presents results through tabs for an interactive map, algorithm iteration curves, performance comparison charts, and detailed text reports.

---

### Results Visualization Showcase

#### 1. Interactive Geographic Route Map

After optimization, the system generates a detailed interactive HTML map using the `Folium` library. Users can zoom, pan, and click on elements within a web browser to intuitively inspect every detail of the planned routes.

![f749df2b40efa8b0afae3704661983d9](https://github.com/user-attachments/assets/376e8da5-029f-4d60-9cc5-fdc66e6c9db2)

> **Map Legend**:
> * **Dark Blue Square**: First-echelon Depot
> * **Green Circle**: Second-echelon Sales Outlet
> * **Orange Pin**: End Customer
> * **Bold Solid Line**: First-echelon truck route (Depot to Outlet)
> * **Thin Solid Line**: Second-echelon truck route (Outlet to Customer)
> * **Dashed Line**: Second-echelon drone delivery route

#### 2. Algorithm Performance Comparison Chart

To facilitate a side-by-side comparison of different algorithms, the system provides intuitive bar charts that evaluate performance based on two key metrics: "Total Cost" and "Makespan."

![5415bc38f44f823ab85defdc074a5117](https://github.com/user-attachments/assets/faf56d82-98d8-4954-a4ad-babfa2fa3329)
![213e76ff12149d24c0084b2624216398](https://github.com/user-attachments/assets/1227fa36-ea27-468c-9f33-76acc94ba6f6)

> **Chart Legend**:
> * **Left Chart (Weighted Cost)**: Compares the final scores of Greedy, Genetic Algorithm, Simulated Annealing, and PSO on the weighted objective function (which combines transport costs, time costs, and penalties). A lower cost indicates a higher-quality solution.
> * **Right Chart (Makespan)**: Shows the time required for the complete simulation of each algorithm, which reflects the algorithm's optimization capability.

---

## Core Features

* **Advanced Problem Modeling**
    * **Two-Echelon Network**: Fully simulates a two-tier delivery network, from central warehouses to secondary outlets and finally to end customers.
    * **Multi-Depot Support**: Supports starting from multiple primary depots to optimize more complex regional logistics networks.
    * **Drone Collaboration**: Allows vehicles and drones to operate in parallel, with drones dispatched from sales outlets to handle short-range, small-parcel deliveries.
    * **Split Deliveries**: Enables a single customer's demand to be fulfilled by multiple deliveries (from different vehicles or drones), improving overall vehicle capacity utilization and efficiency.

* **Powerful Algorithm Suite**
    * **Genetic Algorithm (GA)**: A global search heuristic based on the principles of biological evolution.
    * **Simulated Annealing (SA)**: A probabilistic local search algorithm based on the physical annealing process.
    * **Particle Swarm Optimization (PSO)**: A population-based swarm intelligence algorithm that models the foraging behavior of birds.
    * **Greedy Heuristic**: A fast, constructive heuristic that can be used to generate a baseline solution.

* **Fully-Featured Graphical User Interface (GUI)**
    * **Thread-Safe**: The optimization process runs in a separate background thread, ensuring the GUI remains responsive and avoids freezing during long computations.
    * **Parametric Configuration**: Through an intuitive tabbed interface, users can customize all key parameters, including data generation, vehicle/drone properties, objective function weights, and algorithm-specific hyperparameters.
    * **Configuration Persistence**: Supports saving the current set of parameters to an `.ini` file and loading configurations from a file, facilitating repeatable experiments and sharing of settings.
    * **Real-time Status Feedback**: A status bar at the bottom provides real-time updates on the application's state, such as "Generating data...", "Running Optimization...", and "Optimization Complete".

* **In-Depth Results Visualization & Analysis**
    * **Interactive Geographic Maps**: Generates interactive HTML maps using `Folium` that can be opened in a browser.
    * **Algorithm Iteration Curves**: Uses `Matplotlib` to plot the convergence of the objective function value (cost) during the optimization process.
    * **Multi-Algorithm Performance Comparison**: Provides clear bar charts comparing the final "total cost" and "computation time" across different algorithms.
    * **Detailed Text Reports**: Generates a detailed text report for each algorithm's optimized solution.
    * **Results Export**: All generated charts (iteration curves, comparison plots) and reports can be saved to local files with a single click.

* **Flexible Data Management**
    * **Built-in Data Generator**: Quickly generates synthetic data for testing based on user-defined parameters like the number of depots, outlets, and customers, as well as geographic radius and demand ranges.
    * **Standard Format Compatibility**: Includes a parser framework for the Solomon benchmark dataset, providing the capability to extend support for standard VRPTW benchmarks.

## Project Structure

logistics_optimization/
│
├── main.py                  # Main application entry point, initializes the environment and launches the GUI
├── requirements.txt         # List of project dependencies
├── README.md                # This project description file
│
├── config/                  # Configuration directory
│   └── default_config.ini   # Default parameter configuration file
│
├── core/                    # Core business logic and computation modules
│   ├── cost_function.py     # Objective function (cost, time, penalties) calculation module
│   ├── distance_calculator.py # Geographic distance (Haversine) calculation utility
│   ├── problem_utils.py     # Core problem utilities (solution representation, neighborhood operators, etc.)
│   └── route_optimizer.py   # Optimization process orchestrator, calls algorithms and consolidates results
│
├── data/                    # Data generation and loading modules
│   ├── data_generator.py    # Synthetic data generator
│   └── solomon_parser.py    # Parser for Solomon benchmark datasets
│
├── algorithm/               # Optimization algorithm implementations
│   ├── genetic_algorithm.py # Genetic Algorithm implementation
│   ├── simulated_annealing.py # Simulated Annealing implementation
│   ├── pso_optimizer.py     # Particle Swarm Optimization implementation
│   └── greedy_heuristic.py  # Greedy Heuristic implementation
│
├── gui/                     # Graphical User Interface module
│   └── main_window.py       # Main GUI window, handles all user interactions and workflow control
│
├── visualization/           # Results visualization modules
│   ├── map_generator.py     # Folium interactive map generator
│   └── plot_generator.py    # Matplotlib chart (iteration, comparison) generator
│
└── output/                  # Default directory for saved results


## Installation & Usage

1.  **Clone the Repository**
    ```bash
    git clone <your-repository-url>
    cd logistics_optimization
    ```

2.  **Create and Activate a Virtual Environment (Recommended)**
    ```bash
    # Windows
    python -m venv venv
    venv\Scripts\activate

    # Linux/macOS
    python -m venv venv
    source venv/bin/activate
    ```

3.  **Install Dependencies**
    Install all required libraries from the `requirements.txt` file:
    ```bash
    pip install -r requirements.txt
    ```

4.  **Run the Application**
    Execute `main.py` from the project's root directory to launch the GUI:
    ```bash
    python main.py
    ```

## User Guide

1.  **Configure Parameters (Left Panel)**:
    * Use the **"Data Generation"** tab to set parameters for generating a new problem instance (number of depots, outlets, customers, etc.).
    * In the **"Vehicle"** and **"Drone"** tabs, define the properties of your fleet (payload, speed, cost, drone range, etc.).
    * In the **"Objective"** tab, adjust the weights for cost and time in the objective function and set the penalty for unmet demand.
    * In the **algorithm parameter tabs** (GA, SA, PSO), configure algorithm-specific settings like population size, max iterations, cooling rate, etc..

2.  **Generate/Load Data**:
    * Click the **"Generate Data"** button to create a new set of data points.
    * Click **"Load Config"** to load a previously saved parameter set from an `.ini` file.

3.  **Run Optimization**:
    * In the **"Algorithm Selection & Execution"** section, check the box for one or more algorithms you wish to run and compare.
    * Click the **"Run Optimization"** button to start the process.

4.  **View and Analyze Results (Right Panel)**:
    * **Route Map Tab**:
        * Select a result from the dropdown menu to see its corresponding map information.
        * Click the **"Open Selected Map"** button to view the detailed interactive route map in your browser.
    * **Iteration Curves Tab**: View the cost convergence curves for the heuristic algorithms.
    * **Comparison Tab**: View the bar charts comparing the final cost and computation time for all executed algorithms.
    * **Detailed Report Tab**: Select a result from the dropdown to view its detailed text report.
    * All charts and reports can be saved using the "Save Plot" or "Save Report" buttons.

## Main Dependencies

* **Tkinter** (Python Standard Library): Used for building the Graphical User Interface.
* **Matplotlib**: Used for plotting static charts like iteration curves and comparison graphs.
* **Folium**: Used for generating interactive HTML maps.
* **NumPy**: Used for efficient numerical computations.

---
*This project was developed by Mr. VerseChristi. For questions or data inquiries, please contact versechristi@gmail.com.*
