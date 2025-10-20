---
layout: page
title: "Ant Colony Simulation"
permalink: /projects/ant-colony-simulation/
---

# An Ant Colony's Game of Life

## Project Overview

This project extends Conway's Game of Life principles to simulate competing ant colonies in a grid-based environment. Unlike traditional cellular automata with deterministic rules, this simulation implements mobile agents (ants) with probabilistic decision-making capabilities that mimic real-world ant behaviors including:

- Pheromone trail following
- Territory marking
- Food foraging
- Inter-colony competition

The simulation demonstrates how complex collective behaviors emerge from simple individual rules, providing insights into decentralized multi-agent systems where resource competition and territorial dynamics shape survival outcomes.

## Background & Motivation

Ant colonies operate as decentralized multi-agent systems that achieve complex collective behavior through local interactions. In ecological settings, inter-colony competition plays a critical role in shaping survival outcomes, influencing resource access, territorial boundaries, and long-term species success.

This project addresses the question: **How do competing decentralized ant colonies optimize resource collection and adapt their strategies in response to environmental constraints and rival interference?**

Building on Conway's Game of Life principles, I developed a grid-based simulation framework that extends beyond deterministic cellular automata to model the complex, emergent behaviors of multiple competing ant colonies.

## Technical Implementation

### Core Features
- **Grid-based environment** with configurable dimensions
- **Mobile agents (ants)** with probabilistic movement decisions
- **Pheromone system** for trail formation and territory marking
- **Food generation** with clusters and expiration mechanics
- **Colony reproduction** based on food collection
- **Inter-colony conflict** with aggression thresholds and battle resolution

### Key Technical Components

The simulation includes 49 configurable parameters governing everything from grid size and display settings to ant behavior, pheromone dynamics, food properties, colony characteristics, and conflict outcomes.

#### Sample Parameters:
```python
SIMULATION_CONFIG = {
    # Grid and display settings
    'GRID_WIDTH': 300,            # Width of the grid in cells
    'GRID_HEIGHT': 200,           # Height of the grid in cells
    'CELL_SIZE': 3,               # Size of each cell in pixels
    'FPS': 25,                    # Frames per second
    
    # Ant behavior settings
    'MAX_ANTS': 300,              # Maximum ants per colony
    'MOVEMENT_PROBABILITY': 0.9,  # Chance ants move each tick
    'PHEROMONE_DEPOSIT': 50,      # Food trail strength
    'FOOD_ATTRACTION': 8.0,       # Food influence on movement
    
    # Colony parameters
    'MAX_COLONIES': 5,            # Maximum allowed colonies
    'AGGRESSION_MIN_THRESHOLD': 0.3,  # Minimum aggression threshold
}
```

## Key Findings

The simulation revealed several interesting patterns in colony behavior and competition:

1. **Aggression thresholds significantly impact colony success**:
   - Highly aggressive colonies (threshold ~0.33) showed long-term resilience despite slower initial growth
   - Peaceful colonies (threshold ~0.64) maintained smaller but more stable territories
   - Mid-range aggression (threshold ~0.55) led to rapid early expansion but potential collapse due to overextension

2. **Territory and resource management strategies emerge naturally**:
   - Colonies develop distinct foraging patterns based on competition pressure
   - Pheromone trails create efficient resource gathering networks
   - Territorial boundaries fluctuate based on colony strength and aggression levels

3. **Population dynamics exhibit complex patterns**:
   - Boom-bust cycles emerge from resource competition
   - Battle outcomes significantly impact colony viability
   - Starvation becomes a major limiting factor for overextended colonies

![Colony metrics over time](/assets/images/ant_colony_metrics.png)

## Technologies Used

- **Python**: Core programming language
- **Pygame**: For rendering the simulation and handling user input
- **NumPy**: For efficient grid operations and calculations
- **Pandas**: For data collection and analysis
- **Matplotlib**: For visualizing simulation results

## Code Implementation

The simulation is implemented as a Python application using Pygame for visualization. Here's a snippet showing the core ant movement decision logic:
```python
def select_move(self, grid, food_grid, colony_pheromones):
    # Calculate movement weights based on surrounding cells
    weights = np.ones(8)  # Initialize with equal weights
    
    # Modify weights based on pheromones, food, and current direction
    if self.has_food:
        # Bias toward nest when carrying food
        nest_angle = self.calculate_angle_to_nest()
        dir_weights = self.calculate_direction_weights(nest_angle, INWARD_DIRECTION_WEIGHT)
        weights *= dir_weights
    else:
        # Bias toward exploration when foraging
        weights *= self.calculate_exploration_weights()
    
    # Apply food attraction
    for i, (dx, dy) in enumerate(self.DIRECTIONS):
        nx, ny = self.x + dx, self.y + dy
        if 0 <= nx < grid.shape[1] and 0 <= ny < grid.shape[0]:
            if food_grid[ny, nx] > 0:
                weights[i] *= (1.0 + FOOD_ATTRACTION)
            
            # Apply pheromone influence
            if not self.has_food and colony_pheromones[ny, nx] > 0:
                weights[i] *= (1.0 + PHEROMONE_WEIGHT * min(colony_pheromones[ny, nx], 1.0))
    
    # Normalize weights to form probability distribution
    if np.sum(weights) > 0:
        weights /= np.sum(weights)
        
    # Select direction based on probability distribution
    direction_idx = np.random.choice(8, p=weights)
    return self.DIRECTIONS[direction_idx]
```

## Future Enhancements

Future versions of the simulation could improve biological realism by incorporating:

1. Chemical recognition systems for nestmate identification
2. Adaptive foraging strategies based on past success
3. Terrain features and obstacles
4. Life cycle processes including seasonal variation
5. Multiple ant species with distinct traits

## Conclusion

This simulation demonstrates how complex, adaptive behaviors can emerge from simple rules in a multi-agent system. The decentralized nature of ant colonies provides valuable insights for both ecological understanding and applications in swarm robotics, network routing, and distributed algorithms.

## View the Complete Code

[GitHub Repository](https://github.com/yourusername/ant-colony-simulation)
