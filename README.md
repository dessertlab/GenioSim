# GenioSim
GenioSim is a novel simulation platform to evaluate resource-management and orchestration algorithms. It has been inspired by GENIO (Edge cloud platform enabled by a new intelligent OLT for GPON networks), an industrial R&D project on a new orchestration platform for edge workloads in PON networks.
It is built as an extension of the widely used PureEdgeSim simulator, enriched with new architectural components, virtualization features, and an accurate representation of PON-based access networks.

## Overwiew
GenioSim extends the PureEdgeSim framework to support the simulation of distributed edge infrastructures aligned with the goals of the GENIO project.
GenioSim supports realistic PON topologies, including ONTs,OLTs, and optical fiber links, as well as their hierarchical relationships. Moreover, GenioSim includes native support for hybrid virtualization, enabling simulations of both containers and virtual machines, and introduces a decoupled execution model in which applications (as containers) and user requests (as tasks) follow distinct orchestration flows. These extensions enable the analysis of adaptive orchestration strategies and workload distribution across a realistic PON-enabled infrastructure, in complex and dynamic edge computing scenarios.

## Extension of PureEdgeSim
PureEdgeSim was selected as the foundation due to its flexibility in modeling cloud and edge environments. 
GenioSim enhances it by introducing:

- Multiple link types (optical fiber, MAN, WAN) to capture heterogeneous latency and bandwidth characteristics.
- Custom PON-based topologies, where multiple OLTs, ONTs, and edge devices can be defined.
- Configurable workloads, generated as collections of tasks with parameters such as:
    - maximum latency requirement,
    - task length in millions of instructions (MI),
    - task generation rate,
    - request size and result size.


These extensions enable the simulation of diverse edge applications and orchestration schemes.

## Simulated Application scenarios
Based on the application domains of the GENIO project, GenioSim supports the following scenarios:

- Smart City – smart lighting connected to the same OLT
- E-Health – multiparametric medical monitors
- Smart Building – video-surveillance cameras
- Sports Streaming: 60 users representing simultaneous viewers of live multimedia content;
- Video Gaming: 80 users representing participants in interactive cloud-gaming sessions.

In addition, for orchestration strategy evaluation, we define a Mixed scenario that combines all five baseline applications into a single multi-tenant setup with a total of 298 users, generating heterogeneous and time-varying demand representative of realistic industrial deployments. 

Each scenario is evaluated under different CPU architectures and system configurations.

## Comparing with traditional Edge computing
To compare GENIO with conventional systems, GenioSim includes a baseline configuration representing a traditional edge computing architecture:

- A typical PON topology where the OLT is located at a central office.
- Edge servers and applications are deployed on a remote server.
- OLTs reach the edge servers via 100-meter WAN links.
- The edge layer is therefore split into two separate levels in the simulation.

This provides a meaningful reference point to evaluate GENIO's architectural advantages.

## Evaulation Metrics
GenioSim supports performance evaluation through key metrics:

- Task Latency — the delay between sending a request and completing its processing.
- Task Success Rate (TSR) — the percentage of tasks correctly completed within the simulation time.

These metrics are computed for all simulated application scenarios across different hardware and orchestration strategies.

## Hierarchical Orchestration Architecture
GENIO requires a multi-level orchestration model, implemented in GenioSim.

### Level 1 — Container Placement (Cloud Orchestrator)
Responsible for placing application containers across available nodes, balancing load and respecting placement policies.

### Level 2 — Task Offloading (Edge Orchestrator)
Determines which resource instance (previously placed container) should execute each incoming task.
This layer corresponds to the edge level and is managed by the OLTs.

### DNS-Based Load Balancing
Since GENIO envisions geographically distributed OLTs across a regional area, each edge device may be connected to a different OLT.
To support this, GenioSim models:

- One DNS per OLT, each defined through an XML configuration file.
- DNS responsibilities:
    
    - mapping ONT → OLT,
    - performing load balancing during task offloading.


DNS nodes do not have computational resources; they act purely as load balancers.

## Resource-Management Algorithm Analysis
GenioSim enables the study of resource-management strategies within GENIO-like edge–cloud environments.
The simulator allows researchers to:

- Identify optimal configurations for simple isolated scenarios to maximize theoretical performance.
- Evaluate advanced resource-management algorithms (placement and offloading) in complex scenarios with many decision variables.
- Perform qualitative analysis based on collected metrics such as latency and TSR.
- Assess the impact of factors like network latency, node density, and balancing strategies on overall QoS.

