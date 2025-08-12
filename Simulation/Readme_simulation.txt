# README: Numerical Simulation of Ant Collective Behavior

================================================================================
Overview
================================================================================
'Numerical_simulation_ants.ipynb' is designed to:
- Simulate individual ant trajectories using numerical integration (ODE solvers).
- Implement an ant’s response to local footprint concentration gradients via an empirical perception‐response mechanism.
- Model chemical footprint dynamics (deposition, decay) in a 2D periodic boundary domain.

In this simulation, each ant is a self‐propelled agent moving at constant speed (v0) with stochastic heading updates. 
Ants deposit chemical “footprints” at a production rate (kp) within a deposition radius (ph_r), and the chemical decays at rate (km). 
The ant’s turning is determined by an empirical function that combines:
• An aversion response (parameters K and a) when the sensed lateral gradient is moderate.
• An attraction response (parameters G_tanh and threshold th) when the gradient is strong.

================================================================================
Requirements and Installation
================================================================================

**Python Version**: Python 3.7.

**Required Libraries**:
- numpy
- scipy (version 1.7.3)
- matplotlib
- IPython (for inline display of animations)

================================================================================
Key Simulation Parameters
================================================================================

• n_agents: Number of ants (e.g., 65)
• L: Half-width of the domain (e.g., 0.5, giving a domain of [-0.5, 0.5])
• v0: Ant speed (e.g., 0.02)
• noise_strength: Angular noise standard deviation (e.g., 0.5)
• T_end: Total simulation time (e.g., 200 time units)
• K, a: Aversion parameters (e.g., K = 3.5, a = 10.45)
• G_tanh, th: Attraction parameters (e.g., G_tanh = 0.1, th = 1.0)
• kp: Footprint production rate (e.g., 0.01)
• km: Footprint decay rate (e.g., 0.2)
• ph_r: Footprint deposition radius (e.g., 0.03)
• dx: Grid spacing for the concentration field (e.g., ph_r/3)
• dt: Effective time step (adaptive; max_step ≈ 0.1)

================================================================================
Usage
================================================================================

1. Open `Numerical_simulation_ants.ipynb` in Jupyter Notebook or JupyterLab.
2. Adjust the parameters in the "Parameter Setup" section as needed.
3. Run all cells sequentially to perform the simulation.
4. Outputs include:
   - An animation showing ant trajectories (with velocity arrows) and the evolving chemical footprint field.
   - Plots of local density distributions and mean squared displacement (MSD) over time.
5. Analyze the emergent behaviors (e.g., clustering and diffusive properties) by comparing different parameter settings.
