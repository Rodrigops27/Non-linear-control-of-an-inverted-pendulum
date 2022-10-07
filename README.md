# Non-linear-control-of-an-inverted-pendulum
Decoupling Linearizing control for the classic inverted pendulum with MATLAB and Simulink.

A. MODEL OF THE SYSTEM

The process under interest is an inverted pendulum and is described in the following figure.

![image](https://user-images.githubusercontent.com/92366584/194646431-bbdcd3ff-f57e-4ba8-b940-e51679257209.png)


The process consists of a crane driven by a motor, and moving along a guide rail with a  length of 1m. On this crane, is placed a pendulum with two rods rotating freely, equipped with weights at their tips. Two incremental encoders allow to know the position of the crane and the angle of the pendulum. Safety stops are located at the end of the way on which the crane is moving.

B. MODELLING OF THE INVERTED PENDULUM

The diagram just below (Figure 2) details the physical parameters of the system. In the sequel,  several models will be used, depending on modeling assumptions. Let θ the angle between the pendulum and the vertical, and x the position of the crane. The parameters of the pendulum are the mass of the crane M (=2.4kg), the mass centered at the end of the pendulum m (=0.23kg) and the length of the pendulum L (= 0.36m).

![image](https://user-images.githubusercontent.com/92366584/194646835-a8220688-4f41-4de0-9866-6169d80ac7d2.png)

C. PROBLEM STATEMENT

The objective consists in controlling the motion of the inverted pendulum. The controller needs to control the crane position and the angle of the pendulum (for example, one wants to move the carriage bearing the pendulum at a constant angle).

Model 1 : It is assumed that the system has 2 inputs, there is no friction (dry or viscous) and one neglects the inertia of the pendulum. The control inputs are the driving force of the carriage u1 and the torque of the pendulum u2. It should be noted that in the real application, the control input u2 does not exists, and should therefore be considered equal to 0.

The dynamics reads as:

![image](https://user-images.githubusercontent.com/92366584/194647338-15ec1ec8-9c11-4608-a030-9eb20b2998ca.png)


The first model under nonlinear state system (with x1 = x, x2=dx/dt, x3=q, x4=dq/dt.) is defined as:
![image](https://user-images.githubusercontent.com/92366584/194647287-5ee266ab-fb33-4cd6-909c-3a4f69f873b9.png)

Setting the I/O linearization as:
![image](https://user-images.githubusercontent.com/92366584/194648322-e80beb2c-5b02-4aa5-9c83-6e9d0b454dd8.png)
Remark : the control law reads as u = F(x) + G(x) v with v = [v1 v2]T. This control allows pole placement.
![image](https://user-images.githubusercontent.com/92366584/194649396-808a6549-a61e-4550-8a86-5897c8895dcb.png)

Which logically stabilizes this model 1:
![image](https://user-images.githubusercontent.com/92366584/194647580-9ac56b0b-ef5c-4d80-ab5e-62b86715425c.png)

Model 2 : One suppose now that the system has a single input (u2 = 0) , that there is no friction (dry or viscous) and the pendulum inertia is supposed negligible.
![image](https://user-images.githubusercontent.com/92366584/194650910-c8d58f5b-77e6-4fbd-b8ab-f78e397257fb.png)

In order to analyze the stability of this model, we will require to check the zero dynamics, which are:

![image](https://user-images.githubusercontent.com/92366584/194653135-0f71dc13-602b-46d8-9eea-81a05a5c4fcf.png)

Clearly showing that the state x1 will be "uncontrollably" increasing.
![image](https://user-images.githubusercontent.com/92366584/194650963-021805f2-04bc-4f18-8cef-8738dad2b1cb.png)

Model 3 : Taking into account the friction and inertia of the pendulum.
![image](https://user-images.githubusercontent.com/92366584/194653891-9fd6d0f3-cb93-46bf-8ffa-48088fd4098e.png)

With the aim of design a control law based on a linearizing strategy, allowing to stabilize the both variables, crane position and pendulum angle and tuning the parameters of the controller in order to satisfy the control saturations.
Since the "internal" state x1 increase/decrease, according to the sign of x2, "internally", one option would be to add to the pole placement (the last loop) a feedback control for the position, v=...-k1x1:

![image](https://user-images.githubusercontent.com/92366584/194663164-06c622bf-29ce-4da7-bd59-6ea39b4bf1d4.png)

In this case using x1* and x3* as the reference signal, for a desired position or angle.

Tuning k1 to 0.319 for the model 3, with this "acceptable" behavior:
![image](https://user-images.githubusercontent.com/92366584/194659949-af67ee2b-ebdb-4719-9f69-73ff75b936b8.png)





Project developed under the M1_EPICO_COSYS Control system class leaded by Frank Plestan at École Centrale de Nantes.
All rights reserved to them.
For the original formulation of the models check SUJ_PEND_21_22.pdf
