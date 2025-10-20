---
layout: default
---
   
# Data Science Portfolio
Welcome to my portfolio! Here you'll find a collection of my data science projects.
   
## Projects
   
### Project 01: [Ant Colony Simulation]
Ant colonies operate as decentralized multi-agent systems that achieve complex collective behavior through local interactions. Building on Conway's Game of Life principles, I developed a grid-based framework to simulate competing ant colonies, implementing mobile agents (ants) with probabilistic decision-making capabilities that mimic real-world ant behaviors. This project addresses the question: *How do competing decentralized ant colonies optimize resource collection and adapt their strategies in response to environmental constraints and rival interference?*

#### Technical Implementation
The simulation includes 49 configurable parameters governing everything from grid size and display settings to ant behavior, pheromone dynamics, food properties, colony characteristics, and inter-colony conflict outcomes. The simulation is implemented as a Python application using Pygame for visualization. Here’s a snippet showing the core ant movement decision logic:

```
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

#### Visualizations
This GIF shows a brief recording of the grid-based, ant environment:
![Anthills GIF](/assets/images/ant-images/anthills.gif)

Data analyzing ant behaviour was collected using Pandas during runs of the simulation, which would be vital for simulation-based analysis:
![Anthills GIF](/assets/images/ant-images/food_collected_chart.png)
![Anthills GIF](/assets/images/ant-images/territory_size_chart.png)
![Anthills GIF](/assets/images/ant-images/starved_ants_chart.png)

#### Key Findings

The simulation revealed several interesting patterns in colony behavior and competition:

1. **Aggression thresholds significantly impact colony success**:
   - Highly aggressive colonies (threshold ~0.33) showed long-term resilience despite slower initial growth
   - Peaceful colonies (threshold ~0.64) maintained smaller but more stable territories
   - Mid-range aggression (threshold ~0.55) led to rapid early expansion but potential collapse due to overextension

2. **Territory and resource management strategies emerge naturally**:
   - Colonies develop distinct foraging patterns based on competition pressure
   - Pheromone trails create efficient resource gathering networks
   - Territorial boundaries fluctuate based on colony strength and aggression levels

### Future Enhancements

Future versions of the simulation could improve biological realism by incorporating:

1. Chemical recognition systems for nestmate identification
2. Adaptive foraging strategies based on past success
3. Terrain features and obstacles
4. Life cycle processes including seasonal variation
5. Multiple ant species with distinct traits

### Conclusion

This simulation demonstrates how adaptive behaviors can emerge from simple rules in a multi-agent system. The decentralized nature of ant colonies provides valuable insights for both ecological understanding and applications in swarm robotics, network routing, and distributed algorithms.

