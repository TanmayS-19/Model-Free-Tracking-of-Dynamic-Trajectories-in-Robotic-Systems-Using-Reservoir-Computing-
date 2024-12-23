# Model Free Tracking of Dynamic Trajectories in Robotic Systems Using Reservoir Computing

## Introduction  
The modeling and control of complex dynamical systems pose significant challenges due to their high-dimensional nature and non-linear dynamics. Our project leverages **Reservoir Computing (RC)**, a computational framework ideal for tasks involving temporal data. Using RC, we aim to predict the torques necessary to follow a given trajectory, whether mathematically defined or dynamically generated. This approach demonstrates the versatility of RC in efficiently handling partial state vectors, making it a lightweight yet powerful tool for modeling complex systems.  

## Data Generation  

### Mathematically Defined Trajectories  
Data for mathematically defined trajectories is generated using predefined equations like circular, elliptical, or figure-eight paths. For each trajectory:  
1. **Define the governing mathematical equation** (e.g., a circle: \( x = r \cos(\theta), y = r \sin(\theta) \)).  
2. Sample the time variable \( t \) at fixed intervals to compute corresponding \( x \) and \( y \) positions.  
3. The resulting positions are normalized to ensure consistency in scaling.  

Example: Generating five points for a circular trajectory with radius \( r = 1 \):  
- At \( \theta = 0, \frac{\pi}{2}, \pi, \frac{3\pi}{2}, 2\pi \), we get:  
  \[
  (1, 0), (0, 1), (-1, 0), (0, -1), (1, 0)
  \]  

Velocity values (\( \dot{x}, \dot{y} \)) are computed as derivatives of position with respect to time, providing additional features for training.  

### Dynamic Trajectories  
Dynamic trajectories, such as those derived from Lorenz or Mackey-Glass systems, are simulated from differential equations. For example, the **Lorenz System** is governed by:  
\[
\frac{dx}{dt} = \sigma (y - x), \quad \frac{dy}{dt} = x(\rho - z) - y, \quad \frac{dz}{dt} = xy - \beta z
\]  
1. **Simulate the system** using chosen parameter values (e.g., \( \sigma = 10, \rho = 28, \beta = 8/3 \)).  
2. Normalize the state vectors to a consistent range.  
3. Interpolate the resulting trajectory to achieve a meaningful resolution.  

Example: Five points for the Lorenz trajectory simulated over \( t = 0.01 \) seconds:  
- High-dimensional vectors such as \( (x, y, z) \) are normalized and interpolated to produce meaningful time steps.  

### Partial State Vector
For both mathematically defined and dynamic trajectories, we utilize a four-dimensional partial state vector:

$$[C_x, C_y, \dot{q}_1, \dot{q}_2]^T$$

This partial representation is computationally efficient and reduces the data requirement, making RC particularly suited for such tasks. By focusing on partial states, the complexity of training is reduced without sacrificing predictive accuracy, which is a key advantage of our approach.


## Reservoir Computing  

Reservoir Computing is a neural network framework specifically designed for handling temporal and sequential data. Its architecture consists of:  
1. **Reservoir Layer**: A fixed, high-dimensional dynamical system that projects input data into a nonlinear feature space.  
2. **Output Layer**: A trainable linear layer that maps the reservoir states to the target output.  

### Relevance to Our Project  
- RC effectively handles temporal dependencies, making it suitable for modeling complex dynamical trajectories.  
- The lightweight training process, which only updates the output layer, aligns with the need for efficient learning in high-dimensional systems.  
- The partial state vector as input aligns with RC’s ability to work with sparse representations.  

## Training Phase  

The training phase begins with applying **random torques** to the system. The process can be described step-by-step:  
1. **Initial State**: Start at a randomly chosen point in the state space.  
2. **Apply Random Torques**: For each time step \( t \), apply a randomly generated torque.  
3. **State Transition**: Use the applied torque to transition from state \( t \) to \( t+\Delta t \).  
4. **Record Data**: Combine the state vectors for \( t \) and \( t+\Delta t \) to create a training example.  
5. **Loss Function**: The RC model predicts the applied torques, and the loss function minimizes the difference between actual and predicted torques.  

This iterative process generates a random walk-like trajectory, which constitutes a single episode (\( T_{ep} \)). Multiple episodes are used to train the model to generalize across different trajectories.  

## Testing Phase  

During testing, the model is evaluated on its ability to predict torques for complex, pre-defined trajectories. The process includes:  
1. **Input Data**: Provide the model with known state vectors from the trajectory.  
2. **Torque Prediction**: The model predicts the required torques to transition to the next state.  
3. **Evaluation**: The accuracy of the model is assessed across 16 different complex trajectories, including both mathematically defined and dynamic systems.  

Unlike the training phase, the testing phase involves pre-defined trajectories, allowing us to evaluate the model’s predictive capabilities on unseen data.  

## Conclusion  

Our model demonstrates the efficacy of Reservoir Computing in handling complex dynamical systems. Key advantages include:  
- **Efficiency**: Leveraging partial state vectors reduces computational costs.  
- **Flexibility**: Applicability to diverse trajectories, both mathematically defined and dynamically simulated.  
- **Accuracy**: High predictive accuracy in both training and testing phases.  

### Real-World Applications  
- **Robotics**: Precise trajectory planning for robotic arms and autonomous vehicles.  
- **Climate Modeling**: Simulating chaotic weather systems using Lorenz dynamics.  
- **Industrial Automation**: Optimizing control systems for manufacturing processes.  

This project highlights the versatility and efficiency of Reservoir Computing as a tool for modeling and controlling complex dynamical trajectories.  
