# Model Free Tracking of Dynamic Trajectories in Robotic Systems Using Reservoir Computing

## Introduction  
The modeling and control of complex dynamical systems pose significant challenges due to their high-dimensional nature and non-linear dynamics. Our project leverages **Reservoir Computing (RC)**, a computational framework ideal for tasks involving temporal data. Using RC, we aim to predict the torques necessary to follow a given trajectory, whether mathematically defined or dynamically generated. This approach demonstrates the versatility of RC in efficiently handling partial state vectors, making it a lightweight yet powerful tool for modeling complex systems.  

## Data Generation  

### Mathematically Defined Trajectories  
Data for mathematically defined trajectories is generated using predefined equations like circular, elliptical, or figure-eight paths. For each trajectory:  
1. **Define the governing mathematical equation**

Eg- A circular reference trajectory is periodic, which can be described as

![image](https://github.com/user-attachments/assets/fa8baa05-ba70-46ae-a090-e66d59941a5a)
 
![image](https://github.com/user-attachments/assets/6b79dc7d-a192-4008-990b-efb3f0e2ffeb)

### Dynamic Trajectories

 The classic Lorenz chaotic system, a simplified model for atmospheric convection, is

 ![image](https://github.com/user-attachments/assets/c46c8b6f-890c-40fd-8c0d-dfc389a1409f)

![image](https://github.com/user-attachments/assets/7e5c5284-c26d-4b6f-bba3-5f27991c0c94)

![image](https://github.com/user-attachments/assets/bc8fc082-a9d0-4c16-bac1-17cecbc13c30)

### Partial State Vector
For both mathematically defined and dynamic trajectories, we utilize a four-dimensional partial state vector:

![image](https://github.com/user-attachments/assets/078dc431-387c-4988-92a0-2d32eb97aec5)


## Reservoir Computing  

Reservoir Computing is a neural network framework specifically designed for handling temporal and sequential data. Its architecture consists of:  
1. **Reservoir Layer**: A fixed, high-dimensional dynamical system that projects input data into a nonlinear feature space.  
2. **Output Layer**: A trainable linear layer that maps the reservoir states to the target output.  

### Relevance to Our Project  
- RC effectively handles temporal dependencies, making it suitable for modeling complex dynamical trajectories.  
- The lightweight training process, which only updates the output layer, aligns with the need for efficient learning in high-dimensional systems.  
- The partial state vector as input aligns with RC’s ability to work with sparse representations.  

## Training Phase 

![image](https://github.com/user-attachments/assets/835b6ddf-2d2e-46f5-a1da-af36d2c62cc8)

![image](https://github.com/user-attachments/assets/15eafd42-043f-4a0b-93cc-2ad7b38028b3)

The training phase begins with applying **random torques** to the system. The process can be described step-by-step:  
1. **Initial State**: Start at a randomly chosen point in the state space.  
2. **Apply Random Torques**: For each time step t, apply a randomly generated torque. 
3. **State Transition**: Use the applied torque to transition from state t to t+ Delta t.  
4. **Record Data**: Combine the state vectors for t and t+Delta t to create a training example.
5. **Loss Function**: The RC model predicts the applied torques, and the loss function minimizes the difference between actual and predicted torques.  

This iterative process generates a random walk-like trajectory, which constitutes a single episode T_ep. Multiple episodes are used to train the model to generalize across different trajectories.

![image](https://github.com/user-attachments/assets/fe9edc5a-53e4-436f-83a2-e985dc076a3b)


## Testing Phase  

![image](https://github.com/user-attachments/assets/f86d7481-e58a-4202-a351-76ee3853b466)

During testing, the model is evaluated on its ability to predict torques for complex, pre-defined trajectories. The process includes:  
1. **Input Data**: Provide the model with known state vectors from the trajectory.  
2. **Torque Prediction**: The model predicts the required torques to transition to the next state.  
3. **Evaluation**: The accuracy of the model is assessed across 16 different complex trajectories, including both mathematically defined and dynamic systems.  

Unlike the training phase, the testing phase involves pre-defined trajectories, allowing us to evaluate the model’s predictive capabilities on unseen data.

![image](https://github.com/user-attachments/assets/58fbbc6b-0b49-42e4-8f6c-81e5a9555065)

![image](https://github.com/user-attachments/assets/c4943c30-ead0-4c08-9c98-5e37dc89c51a)

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
