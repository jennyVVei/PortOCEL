# PortOCEL - A Synthetic Port Logistics Dataset Integrating Real-World Business Processes and IoT Data
This repository contains the simulation code, supporting files, and a synthetic IoT-enriched Object-Centric Event Log (OCEL) of the cargo pickup process at a major Chinese port.

The dataset was generated through a Coloured Petri Net (CPN) simulation of the cargo pickup process. Synthetic sensor data and initial process objects were prepared before the simulation. During the simulation, process events, objects, their relationships, and IoT observations were recorded in CSV files. These files were subsequently transformed into an OCEL 2.0 SQLite database using the PM4Py Python package.

## Dataset

The final synthetic IoT-enriched OCEL is provided as an OCEL 2.0 SQLite database:

```text
truck_bp_iot/CargoPickup_IoT.sqlite
```

The dataset contains the simulated cargo pickup process, including process events and objects, their relationships, and associated IoT observations.

In addition to the final SQLite database, the repository includes the intermediate CSV files generated during the simulation and the files used to generate the dataset.

## Repository Structure

```text
.
├── object_initialiser_iot/
│   ├── object_initialisation_iot.cpn
│   ├── logistics_object_initialiser.sml
│   ├── object.csv
│   ├── object_map_type.csv
│   ├── object_Cargo.csv
│   ├── object_Pickupplan.csv
│   ├── object_Silo.csv
│   └── object_Truck.csv
│
├── truck_bp_iot/
│   ├── truck_bp_iot_Fraud_updated_final.cpn
│   ├── logistics-time-utils.sml
│   │
│   ├── event.csv
│   ├── event_map_type.csv
│   ├── event_*.csv
│   │
│   ├── object.csv
│   ├── object_map_type.csv
│   ├── object_*.csv
│   │
│   ├── event_object.csv
│   ├── object_object.csv
│   ├── event_IoTobject.csv
│   ├── object_IoTobject.csv
│   │
│   ├── InfraredSensorRecord.csv
│   ├── TruckGPSRecord.csv
│   ├── TruckHistoryWeightRecord.csv
│   │
│   ├── CSVs_to_OCEL_SQLITE.ipynb
│   └── CargoPickup_IoT.sqlite
│
├── Sensor_data_generation.ipynb
├── weight_sensor_data.csv
├── Reshaped_Silo_IoT_Data_with_dewpoint_prob.csv
└── hourly_rainfall_data.csv
```

### `object_initialiser_iot/`

Contains the CPN model and supporting files used to initialise the process objects required by the cargo pickup simulation, including cargo, pickup plans, silos, and trucks.

### `truck_bp_iot/`

Contains the main CPN model for the cargo pickup process, supporting SML functions, simulation outputs, and the notebook used to construct the final OCEL.

The simulation outputs include:

- **Event data** — `event.csv`, `event_map_type.csv`, and event-type-specific CSV files.
- **Object data** — `object.csv`, `object_map_type.csv`, and object-type-specific CSV files.
- **OCEL relationships** — `event_object.csv` and `object_object.csv`.
- **IoT-enrichment relationships** — `event_IoTobject.csv` and `object_IoTobject.csv`.
- **IoT records** — `InfraredSensorRecord.csv`, `TruckGPSRecord.csv`, and `TruckHistoryWeightRecord.csv`.

The event, object, event–object, and object–object tables are structured in accordance with the OCEL 2.0 relational schema. The additional `event_IoTobject.csv` and `object_IoTobject.csv` tables represent relationships introduced for IoT enrichment.

`InfraredSensorRecord.csv` and `TruckGPSRecord.csv` contain IoT observations generated during the CPN simulation, while `TruckHistoryWeightRecord.csv` contains historical truck weight records that were updated during the simulation.

### Synthetic Sensor Data

The following synthetic sensor and environmental datasets were used by the CPN simulation:

- `weight_sensor_data.csv`
- `Reshaped_Silo_IoT_Data_with_dewpoint_prob.csv`
- `hourly_rainfall_data.csv`

These files were generated using `Sensor_data_generation.ipynb`.

## Data Generation Workflow

The dataset was generated through four main stages:

1. **Synthetic sensor data generation**  
   `Sensor_data_generation.ipynb` was used to generate the synthetic weight, silo, and rainfall data used by the simulation.

2. **Object initialisation**  
   The CPN model in `object_initialiser_iot/` was used to initialise the process objects required for the cargo pickup simulation.

3. **Cargo pickup process simulation**  
   The main CPN model in `truck_bp_iot/` was used to simulate the cargo pickup process and record the resulting events, objects, relationships, and IoT observations as CSV files.

4. **OCEL construction**  
   `truck_bp_iot/CSVs_to_OCEL_SQLITE.ipynb` was used to transform the simulation outputs into the final OCEL 2.0 SQLite database.


> **Note:** The repository structure reflects the relative file paths used by the CPN models and supporting SML code and should therefore be retained when running the simulation. The data-generation procedure contains stochastic elements; consequently, rerunning the simulation may produce a synthetic dataset that differs from the dataset released in this repository.
