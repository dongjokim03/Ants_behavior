# README: Ant Collective Behavior — Training and Analysis

This project aims to model the collective movement behavior of ants by learning how individual ants perceive and respond to "footprint" trails. 
In other words, the code infers a perception-response mechanism from experimental data of ant trajectories. 
It uses a combination of neural network models and constraints:
- The ants’ trajectories over time.
- The spatiotemporal footprint field (modeled via a PDE).
- The ants’ response strategy to the footprint (modeled as a neural network function mapping sensed concentration gradients to changes in movement).

By training these components on real ant colony trajectory data, the project uncovers the rules governing ant collective movement. 
The overall goal is to replicate observed ant trails and infer how ants collectively move via environmental signals. 

================================================================================
Project Files
================================================================================

1. Training_experimental_trajectory.ipynb
   - Purpose: Trains a neural network model to fit the experimental ant trajectories.
   - Functionality:
     - Loads experimental data (e.g., from 0620_L_listX and  0620_L_listY.csv) containing ant positions. (**please download from 'https://zenodo.org/records/16797507')
     - Filters the data (e.g., Colony 620 and SizeClass 'L').
     - Trains a baseline trajectory model (PINN_ODE) on segmented time intervals (e.g., 100-second segments).
     - Saves each segment’s trained model to the Model/ODE/ folder.
   - Usage: Run the notebook to obtain baseline trajectory models that capture the ants’ motion.

2. Training_footprint_and_perception-response.ipynb
   - Purpose: Trains an integrated model to learn both the footprint concentration field and the ants’ response mechanism.
   - Functionality:
     - Loads the previously trained trajectory models.
     - Computes the ants’ speed and uses a Gaussian Mixture Model to determine an active movement threshold.
     - Trains two coupled neural networks:
       - A PINN_PDE for the footprint concentration field (constrained by a PDE).
       - A Mechanism_NN that maps footprint concentration gradients to ant turning rate.
     - Iterates over each time segment, evaluating losses (trajectory fit, PDE residual, response error) and saving models to Model/PDE/.
   - Usage: Run after the trajectory training to learn the integrated perception-response behavior.

3. Selective_averaging.ipynb
   - Purpose: Aggregates the results of multiple training runs to derive an average perception-response function.
   - Functionality:
     - Loads the saved all models for each group (e.g., Colony 620 and SizeClass 'L').
     - Evaluates model for each time interval.
     - Computes and plots the mean response curve with standard deviation bounds.
   - Usage: Run to obtain a robust, averaged representation of the ants’ response to pheromone gradients.

4. Trained_model_load_and_visualization.ipynb
   - Purpose: Loads the trained models and visualizes their performance.
   - Functionality:
     - Loads the baseline trajectory model (PINN_ODE) and the integrated models (PINN_PDE and Mechanism_NN) for a selected time segment.
     - Generates visualizations such as:
       - Animated ant trajectories.
       - Animated pheromone concentration field heatmaps.
       - Possibly static plots comparing predictions with experimental data.
     - Saves animations as MP4 files in the Video/ directory.
   - Usage: Run to visually inspect the model outputs and validate performance.
