## Master's Thesis
- Keywords: robot tasks, reinforcement learning algos and hps, sim2real transfer, landscape visualization.
- Details:
1. Define three robot tasks: reach, push, pnp. Select two algorithms: SAC and PPO. Select two hyperparameters: learning rate and discount factor. 
2. Find and tailor the simulation environment to the real robot environment.
3. Do the trial training of one combination of algos and hps on the simulation to find the suitable reward function and the total time consumption.
4. Train many combinations for each robot task on the simulation over a cloud-server.
5. Implement the trained models on the real robot environment and compare between the performance on simulation and real.
6. Evaluate the results and build a landscape visualization to show the effect of algos and hps on Sim2Real Transfer.
- Facts:
1. Using SAC algorithm for reach task. Middle learning rate and lower discount factor to have the minimal Sim2Real transfer. Which means it performs the best in real when it already performs well in simulation.
2. But the results from my research don't use the model trained very compeletely on simulation and don't have very various kombinations because of timelimit.
## Student Project
- Keywords: data processing, deep learning models, computer vision, image and lidar point cloud.
- Details:
1. Annotating the images with the label of cars and pedestrians.
2. Find and tailor the dl models for traffic participants.
3. Train the dl models with the annotated images.
4. Transfer the 2D to 3D using intrinsic and extrinsic matrix based on coordinationsrelation.
5. Compare 3D results with the 3D point cloud and find the correspond points on lidar.
6. Remove unusual points like outliers and points of floor.
7. Compute the 3D position and orientation
- 
