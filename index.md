---
layout: default
---
   
# Data Science Portfolio
Welcome to my portfolio! Here you'll find a collection of my data science projects.
   
## Projects
   
### Project 01: [Ant Colony Simulation](projects/ant-colony-simulation/)
Ant colonies operate as decentralized multi-agent systems that achieve complex collective behavior through local interactions. In ecological settings, inter-colony competition plays a critical role in shaping survival outcomes, influencing resource access, territorial boundaries, and long-term species success. This project extends Conway's Game of Life principles to simulate competing ant colonies in a grid-based environment, implementing mobile agents (ants) with probabilistic decision-making capabilities that mimic real-world ant behaviors.

This project addresses the question: **How do competing decentralized ant colonies optimize resource collection and adapt their strategies in response to environmental constraints and rival interference?**

Building on Conway's Game of Life principles, I developed a grid-based simulation framework that extends beyond deterministic cellular automata to model the complex, emergent behaviors of multiple competing ant colonies.

#### Technical Implementation
The simulation includes 49 configurable parameters governing everything from grid size and display settings to ant behavior, pheromone dynamics, food properties, colony characteristics, and inter-colony conflict outcomes.

##### Sample Parameters:
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
}
```

### Visualizations

![Colony metrics over time](/assets/images/ant-images/anthills.gif)

### Key Findings

The simulation revealed several interesting patterns in colony behavior and competition:

1. **Aggression thresholds significantly impact colony success**:
   - Highly aggressive colonies (threshold ~0.33) showed long-term resilience despite slower initial growth
   - Peaceful colonies (threshold ~0.64) maintained smaller but more stable territories
   - Mid-range aggression (threshold ~0.55) led to rapid early expansion but potential collapse due to overextension

2. **Territory and resource management strategies emerge naturally**:
   - Colonies develop distinct foraging patterns based on competition pressure
   - Pheromone trails create efficient resource gathering networks
   - Territorial boundaries fluctuate based on colony strength and aggression levels

### Technologies Used

- **Python**: Core programming language
- **Pygame**: For rendering the simulation and handling user input
- **NumPy**: For efficient grid operations and calculations
- **Pandas**: For data collection and analysis
- **Matplotlib**: For visualizing simulation results

### Future Enhancements

Future versions of the simulation could improve biological realism by incorporating:

1. Chemical recognition systems for nestmate identification
2. Adaptive foraging strategies based on past success
3. Terrain features and obstacles
4. Life cycle processes including seasonal variation
5. Multiple ant species with distinct traits

### Conclusion

This simulation demonstrates how adaptive behaviors can emerge from simple rules in a multi-agent system. The decentralized nature of ant colonies provides valuable insights for both ecological understanding and applications in swarm robotics, network routing, and distributed algorithms.

