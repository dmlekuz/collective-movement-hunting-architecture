# Agent-Based Model of Collective Herd Movement and Hunting Architecture

This repository contains the NetLogo implementation of an agent-based model used to explore how architectural geometry shapes collective animal movement in large-scale prehistoric hunting structures.

The model investigates how simple interaction rules, combined with architectural constraints and directional pressure from human or canine drivers, give rise to distinct movement regimes and capture outcomes. It is designed to isolate **geometric effects on collective dynamics**, rather than to reconstruct specific historical hunts.

## Model overview

The model simulates a herd of moving agents (“deer”) interacting locally through cohesion, alignment, and separation rules, extended with a transient excitation (panic) state. Movement is influenced by:

- local herd interactions,
- excitation contagion and decay,
- avoidance of drivers (humans and/or dogs),
- guidance by architectural elements (walls, funnels, necks).

Architecture is implemented as static spatial constraints that bias trajectories through tangent-following avoidance rather than physical blockage. Capture occurs when agents enter a defined terminal zone downstream of the architectural structure.

The model builds on the standard NetLogo flocking example and introduces additional dynamics relevant to herding, stress propagation, and spatial constraint.

## Simulation domain

The simulation domain consists of a 200 × 200 patch grid and is open. Herd agents may exit the domain freely, representing escape. The simulation terminates when all agents have either entered the capture zone or exited the domain.

## Architectural elements

- Walls are manually drawn as patch-based line segments.
- Funnel arms, straight barriers, and terminal necks can be configured.
- Walls do not block movement; agents steer tangentially along them.
- A circular capture zone removes agents from the simulation and records capture events.

Architectural geometry is treated as an experimental variable.

## Parameters and experiments

Default parameters are chosen to produce stable herding behavior under baseline conditions while allowing sensitivity to spatial constraint. Typical experiments involve:

- 500 herd agents per run,
- 100 stochastic runs per architectural configuration,
- variation in wall geometry (straight walls, shallow funnels, steep funnels, with or without terminal necks).

Detailed parameter descriptions and sensitivity analyses are provided in the Supplementary Information accompanying the associated paper.

## Agents

### Herd agents (“deer”)
- Self-propelled agents with limited field of vision.
- Interact locally via separation, alignment, and cohesion.
- Maintain an internal excitation (panic) state that modulates turning, speed, and responsiveness.
- Respond to drivers and architectural elements through avoidance and guidance behaviors.

### Driver agents (“drivers”)
- Represent humans and/or dogs acting collectively.
- Do not directly control individual animals.
- Form a laterally distributed driving front behind the herd.
- Bias movement direction through avoidance-induced excitation rather than direct force.


## Model logic (high-level)

At each time step, herd agents:
- Identify nearby neighbors within a wide field of vision.
- Apply flocking rules (separation, alignment, cohesion).
- Update excitation based on local interactions, driver proximity, and impeded motion.
- Avoid drivers and steer away from them under excitation.
- Respond to walls via tangent-following guidance.
- Move according to speed scaled by excitation.
Check for capture.

Drivers reposition continuously behind the herd and maintain separation from one another.

## Outputs

During simulation, agents log activity to spatial patches, including:
- visit frequency,
- cumulative excitation,
- summed movement vectors.

At the end of each run, patch-level data are exported as CSV files for further analysis and visualization.

## Usage

1. Open the model in **NetLogo** (version compatible with NetLogo 7.0).
2. Adjust parameters via the interface or code as drawded.
3. Setup  architectural via scripted procedures.
4. Run simulations interactively or using BehaviorSpace for batch runs.
5. Export results for post-processing.

##### Model parameters

Model parameters are defined through a combination of interactive interface controls and fixed global variables.

Key behavioral parameters are exposed as sliders in the NetLogo interface, allowing interactive exploration of herd dynamics. These include population size, vision range, minimum separation distance, maximum turning rates for alignment, cohesion, and separation, as well as maximum speed and acceleration.

Additional parameters governing excitement (panic) dynamics, driver behavior, and architectural interaction (e.g. excitation decay, contagion strength, wall interaction radius) are defined as global variables in the model code. These parameters are held constant across experimental runs unless explicitly varied.

This separation allows core flocking behavior to be explored interactively, while maintaining stable, controlled conditions for systematic experiments reported in the associated paper.

### Defining architecvtural geometry and capture zone

Architectural geometry is defined procedurally by drawing wall segments onto the simulation grid. In a typical funnel configuration, two converging guiding walls are constructed upstream of a short terminal constriction (“neck”), without fully enclosing movement.

Funnel geometry is controlled by a small set of parameters (e.g. entrance width, funnel depth, neck length), and instantiated by calling a scripted procedure (`draw-funnel`) that places wall patches accordingly.

The capture zone is defined independently of wall geometry as a circular patch region located downstream of the funnel or neck. When a herd agent enters the capture zone, it is removed from the simulation and counted as captured.

## Scope and limitations

This model is intended to explore **generic principles of collective movement under architectural constraint**. It does not:
- model species-specific cognition or learning,
- reconstruct particular archaeological events,
- include three-dimensional terrain or long-term landscape dynamics.

Results should be interpreted as **transferable dynamical principles**, not as direct historical reconstructions.

## Citation

If you use or adapt this model, please cite the associated paper:

(Full citation to be updated upon publication.)

## License

MIT

## Author

Dimitrij Mlekuž Vrhovnik  
University of Ljubljana, Faculty of Arts  
Department of Archaeology
dimitrij.mlekuz@ff.uni-lj.si

## Acknowledgements

This model builds on the NetLogo flocking example and draws inspiration from research on collective motion, crowd dynamics, and spatial configuration.
