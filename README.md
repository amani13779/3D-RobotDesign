# 3D-RobotDesign


### 1. Body & Structure Design
* **Chassis Shape:** The robot features a lightweight, rectangular box-shaped chassis. This design provides a spacious internal compartment to securely house the microcontroller, battery, and wiring, while keeping the outer profile clean and easy to 3D print in Tinkercad.
* **Materials & Aesthetics:** The structure is divided into modular shells using neutral colors (White for the main body covers, Metallic Gray for the structural frame, and Matte Black for the front head visor).

### 2. Leg Design
* **Structure:** The robot uses 4 identical, symmetrical legs placed at the corners of the chassis to maximize the support polygon. 
* **Linkage:** Each leg consists of an upper link (thigh) and a lower link (shin) connected in series, mimicking a basic mammal-like leg configuration for efficient stepping.

### 3. Joints & Degrees of Freedom (DoF)
* **Joint Count:** 2 active revolute joints per leg (one at the hip/shoulder and one at the knee), making a total of 8 active joints for the entire robot.
* **Degrees of Freedom (DoF):** Each leg has 2 DoF (Pitch motion only), allowing the leg to move forward, backward, up, and down. The entire robot has a total of 8 DoF, which is sufficient for basic 2D planar walking gaits.

### 4. Motor Selection
* **Actuators:** Standard **SG90 or MG90S Micro Servo Motors** are selected for the joints. 
* **Reasoning:** They are chosen because they are highly compatible with lightweight Tinkercad designs, affordable, easy to control via PWM, and provide adequate torque for a small-scale prototype.

### 5. Initial Joint Torque Calculation
To ensure the selected motors can lift the robot, an initial static torque calculation is done for the knee/hip joint when the leg is fully extended horizontally (worst-case scenario):
* **Estimated Weight ($m$):** $0.4\text{ kg}$ (Total robot mass).
* **Weight per leg ($W_{\text{leg}}$):** Assuming the robot stands on at least 2 legs during a step, each leg holds $0.2\text{ kg}$. 
  $$F = 0.2\text{ kg} \times 9.81\text{ m/s}^2 \approx 1.96\text{ N}$$
* **Max Leg Length ($L$):** $0.08\text{ m}$ (Distance from joint to foot).
* **Required Torque ($\tau$):**
  $$\tau = F \times L = 1.96\text{ N} \times 0.08\text{ m} = 0.1568\text{ Nm} \approx 1.6\text{ kg}\cdot\text{cm}$$
* **Conclusion:** Since the MG90S servo provides a stall torque of around $1.8\text{ to }2.2\text{ kg}\cdot\text{cm}$ (at $4.8\text{V}-6\text{V}$), it is safely capable of handling the initial static load.

### 6. Stability & Center of Gravity (CoG)
* **CoG Placement:** The center of gravity is mathematically centered in the middle of the rectangular chassis, kept as low as possible by placing the heavy components (like the battery) at the bottom base.
* **Static Stability:** The robot maintains static stability during movement by ensuring its CoG projection always falls inside the triangular support polygon formed by the three legs touching the ground.

### 7. Proposed Walking Gait
* **Gait Type:** A standard **Static Crawl Gait (3+1)** is proposed.
* **Movement Sequence:** The robot moves only one leg at a time while keeping the other three firmly on the ground to maintain continuous balance. The body shifts forward dynamically between steps to reposition the CoG safely before the next leg lifts.

### 8. Expected Mechanical Issues
* **Backlash & Play:** Cheap plastic or metal gears in micro servos often have small gaps, causing slight shaking or inaccuracies in leg positioning.
* **Friction & Slipping:** Plastic 3D-printed feet might slip on smooth surfaces. *Solution:* Adding small rubber pads or TPU caps to the feet tips to increase traction.
* **Structural Deflection:** Since the parts are designed simply, thin 3D-printed leg links might bend slightly under stress. The shell thickness must be optimized during slicing to prevent deformation.
