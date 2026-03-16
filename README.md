# GenioSim

GenioSim is a simulation platform for evaluating resource management and orchestration algorithms in PON-enabled edge computing infrastructures.

The simulator was developed within the [GENIO (Edge cloud platform enabled by a new intelligent OLT for GPON networks)](https://sysmanagement.it/en/genius/), an industrial R&D initiative exploring new orchestration architectures for edge workloads deployed over Passive Optical Networks (PON).

GenioSim is implemented as an extension of the widely used [PureEdgeSim simulator](https://github.com/CharafeddineMechalikh/PureEdgeSim).


## Overview
GenioSim extends the PureEdgeSim framework to support the simulation of distributed edge infrastructures built on PON access networks.

The simulator introduces support for:
- hierarchical PON topologies including OLTs and ONTs
- heterogeneous network links (fiber, MAN, WAN)
- hybrid virtualization environments combining containers and virtual machines
- hierarchical orchestration models separating container placement and task offloading
- configurable workloads representing realistic edge applications

These capabilities enable the study of orchestration strategies and resource allocation policies in complex PON-enabled edge computing environments.

## Installation

Clone the repository:
```
git clone https://github.com/dessertlab/GenioSim.git
cd GenioSim
```
Build the simulator:
```
mvn clean package
```

After compilation, the executable simulator will be generated in the target/ directory.


## Running the Simulator

General configuration files used by the simulator are located in the `PureEdgeSim/settings/` folder. Experiment-specific configuration files are located in `PureEdgeSim/examples.ProgettoGenio/ProgettoGenio_settings/`. You can customize the scenario to run by modifying the following files:
- `applications_NameScenario.xml`
- `cloud_NameScenario.xml`
- `edge_datacenters_NameScenario.xml`
- `users.xml`
- `simulation_parameters_NameScenario.properties`


Simulations are executed through the main class:
```
PureEdgeSim/examples.ProgettoGenio/ProgettoGenio.java
```

You can run the simulator either from the command line or through an IDE.

### Running from the command line

```
java -cp target/geniosim.jar examples.ProgettoGenio.ProgettoGenio
```

### Running from an IDE

1. Open the repository in IntelliJ IDEA or VSCode
2. Navigate to PureEdgeSim/examples.ProgettoGenio/ProgettoGenio.java
3. Run the main() method.
4. Simulation logs will appear in the console, and output results will be written to: /Output





## Extension of PureEdgeSim
PureEdgeSim was selected as the base simulator due to its flexibility in modeling cloud and edge computing environments. GenioSim extends it with several new capabilities:

### Network Modeling
- multiple link types (optical fiber, MAN, WAN)
- configurable latency and bandwidth parameters
- hierarchical PON infrastructure

### PON Topology Support
GenioSim models realistic PON deployments including:
- Optical Line Terminals (OLTs)
- Optical Network Terminals (ONTs)
- edge devices connected through the access network

### Hybrid Virtualization
The simulator supports hybrid environments where:
- infrastructure services run inside virtual machines
- application workloads run inside containers

### Workload Modeling
Applications are modeled as streams of tasks with configurable parameters such as:
- maximum latency requirement
- task length (Millions of Instructions)
- task generation rate
- request size
- response size

These features allow modeling heterogeneous edge workloads and orchestration strategies.


## Simulated Application scenarios
Based on the application domains of the GENIO project, GenioSim supports the following scenarios:

- Smart City – Connected smart lighting nodes deployed under the same OLT.
- E-Health – Multiparametric medical monitoring devices generating continuous health data.
- Smart Building – Video surveillance cameras performing analytics tasks.
- Sports Streaming – Users consuming live multimedia streams.
- Video Gaming – Interactive cloud-gaming sessions with strict latency constraints.
- Mixed Scenario – A multi-tenant configuration combining all applications into a single workload with 298 concurrent users, representing realistic heterogeneous demand.

Each scenario can be evaluated under different infrastructure configurations and CPU architectures.


## Baseline Architecture for Comparison
To evaluate the benefits of GENIO architectures, GenioSim also supports a baseline configuration representing traditional edge computing deployments.

In this baseline:
- OLTs remain access aggregation points
- edge applications are deployed on remote servers
- OLTs reach edge servers through WAN links

This configuration allows comparing GENIO's architecture against conventional edge infrastructures.


## Evaulation Metrics
GenioSim evaluates system performance through the following metrics:

- Task Latency - Time between the submission of a user request and completion of its processing.
- Task Success Rate (TSR) - Percentage of tasks completed within the simulation time and respecting the application SLA.

These metrics are collected for all simulated scenarios across different orchestration strategies.

## Hierarchical Orchestration Architecture
GenioSim models a two-level orchestration architecture consistent with the GENIO system design.

### Level 1 — Container Placement
The cloud orchestrator decides where application containers should be deployed across available nodes. This decision balances:

- resource availability
- infrastructure topology
- placement policies

### Level 2 — Task Offloading
Edge orchestrators determine which container instance should execute each incoming task. This layer corresponds to the OLT level of the infrastructure.


### DNS-Based Load Balancing
In GENIO deployments, multiple geographically distributed OLTs serve edge devices. GenioSim models this behavior through DNS-based load balancing. Each OLT has an associated DNS entity responsible for:
- mapping ONTs to OLTs
- balancing incoming workload requests

DNS nodes do not perform computation; they act purely as routing and load-balancing components.



## How to Replicate an Experiment

All experiments described in the paper can be reproduced using the configuration files provided in:
```
PureEdgeSim/examples.ProgettoGenio/ProgettoGenio_settings/
```
Each scenario contains a dedicated folder with configuration files.
Key files include:
```
applications_<scenario>.xml
cloud_<scenario>.xml
edge_datacenters_<scenario>.xml
users.xml
simulation_parameters_<scenario>.properties
```

These files define, respectively:
- application properties
- infrastructure configuration (cloud and edge datacenters nodes)
- user workload
- simulation parameters


To reproduce a specific experiment:
1. Select the desired scenario folder.
2. Open `ProgettoGenio.java`.
3. Set the variable `exampleMode = "<ScenarioName>"`.
4. Select the desired placement and offloading algorithms.
4. Run the simulation.


