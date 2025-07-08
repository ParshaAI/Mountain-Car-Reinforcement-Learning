Overview
This project implements Q-learning on the classic Mountain Car problem with several experimental modifications to the state space discretization and reward structure. The goal is to enable the car agent to learn to reach a target position (the hill) by experimenting with different discretization strategies (one-dimensional binning with position, gradient, additional colour coding, and coarse tiling) and tuning the reward function along with learning parameters.

Experimental Tasks
The experimental study is divided into several tasks, each exploring different aspects of state discretization and learning parameters:

Task 1: Implementing Q-Learning (Basic Position Binning)
Reward Function:

+10 when the car reaches the desired hill position.

-0.01 per step to encourage faster learning.

-5 when moving in the wrong direction.

Additional reward of 0.001 for actions guiding towards the goal.

State Discretization:

The position space is divided into 20 equally spaced bins using np.linspace and np.digitize.

Parameters:

Alpha = 0.1, Gamma = 0.99, Epsilon = 0.04 (with decay 0.995, minimum epsilon = 0.002)

Figures for single run and aggregated 10-run results are included in the report (e.g., Figures 1.1, 1.2, etc.).

Task 2: Gradient State Space
State Discretization:

The continuous gradient values are divided into 60 bins using np.linspace and assigned using np.digitize.

Observations:

This approach provided a finer granularity over the gradient space, though the agent initially struggled with convergence due to a lack of position information.

Results:

Lower average steps compared to Task 1 but a reduced number of successful outcomes.

Task 3: Adding a Garage/Parking Spot
Modification:

Changes in the goal’s position: the agent now targets the valley rather than the top of the hill.

State Discretization:

Remains the same as Task 2 (gradient binning into 60 bins).

Observations:

The performance degrades further due to episode failures when reaching the new goal.

Task 4: Grid Binning Using Two Colours
State Discretization:

Combines gradient (60 bins) with a binary colour coding based on position (green for left, red for right) using a threshold (x_threshold = 0.0).

Observations:

Improved learning efficiency as the agent gains more spatial information, resulting in a lower average step count and more successful outcomes.

Task 5: Additional Colours to Enhance the State Space
State Discretization:

Uses four colours (light green, green, red, light red) to capture different regions along the x-dimension.

Observations:

Although the step count increased (due to more exploration areas), the number of successful outcomes also increased, indicating better-informed decisions by the agent.

Task 6: Coarse Tiling
State Discretization:

Employs overlapping colour regions (coarse tiling) along the x-dimension using the same colours as in Task 5.

Parameter Adjustments:

Epsilon decay was changed to 0.99 and epsilon_min was reduced to 0.001 to control excessive exploration.

Observations:

Overlapping regions helped improve overall successful outcomes while maintaining a comparable average step count to Task 5.

Performance Summary
The following tables summarize the experimental results across the tasks, based on average steps per 10-run experiments and the number of successful outcomes (10 successful outcomes per run over 10 runs):

Task	Average Steps	Successful Outcomes
Task 1	43108.1	85
Task 2	35400.7	56
Task 3	26396.5	36
Task 4	23459.9	64
Task 5	49141.0	72
Task 6	49861.8	79

Note: Lower average steps indicate that episodes terminate faster (due to failure), while a higher number of successful outcomes implies better learning performance.

