Triton Robotics Week 2 Training - Wiring the Robot

This week we will be focusing on how to wire the robot, the most common task another subteam member will ask you to do. Don't worry if you're not able to get it fully correct just after this week you will have plenty of time to practice and eventually memorize the wiring.

We can break down our robot into four main systems
1. Mini PC
2. Chassis
3. Gimbal
4. Ammo

Mini-PC\
This system includes the Nucleo and Jetson which act as the 'brains' of the robot. The Nucleo interprets commands from the controller and sends commands to motors. The Jetson is responsible for all autonomous tasks such as CV or Localization (only on Sentry.) Unlike other systems power to these devices must be lowered using buck converters. 

Chassis\
This system refers to all motors that control a movement wheel on the bottom half of the robot, reffered to as the chassis. There are four wheels and thus four motors. 

Gimbal\
This system is responsible for the movement of the head. This is the pitch motor which controls movement on the vertical axis and the yaw motor which controls movement on the horizontal axis. 

Ammo\
This system includes any motors that enable the robot to shoot. These are the flywheel motors, which push the bullets out of the head, and the indexer which feeds ammo into the head to be shot. 

Each system has it's own power ground and signal which are independently wired. You may be wondering why we split up these systems in this manner. It was not a random choice, these systems interact with the referee system. During competition the referee's check to see if they are able to turn off and on each of these. Turning off one system must not affect the others. 

A function we wish to have on our robot is called bayblading wherein the chassis spins while the head maintains it's position. This is an effective strategy during competition where opponents can only hit specified markers on our robot. In order to accomplish this task we must split the head and chassis into independent systems seperated by a slipring. A slipring is a component which contains wires on either end and each side is able to spin independently. We use the slipring to send power from the battery (located in the chassis) to the nucleo (located in the head.) We also use the slipring to send data from the nucleo to motors located in the chassis (there are other uses which we will touch on later.) On each side of the head there is a breakout board from which other components connect.

There is a seperate component which exists outside of these systems, the encoder. An encoder measures the speed and position of a specific motor. In our current setup we have an encoder connected to our yaw motor. With this encoder we are able to know the position of **yaw at all times,** The encoder connects to the bottom slipring breakout board. 

Let's zoom in for now and look at an individual motor, say the top left chasis motor. If we want this wheel to spin, how do we accomplish that? For the motor to move it requires two components, power and signal. Power is given via the chassis subsystem which is provided power by the battery. Signal must be given by the nucleo, which sends data through a motorcontroller that connects to the motor\
The motor will have two ports, one with black, yellow, and red wires for power and a 6-pin connector for signal. The motorcontroller will have two wires that need to be plugged in, an xt30 for power and a CAN wire for signal. These are the basics that every motor actoss the entire robot will need.\

Now let's introduce the referee system.
In the chassis there contains:
1. The Power Management Module (PMM)
2. The Main Control Module (MCM)
3. Armor modules
5. Lightbar
6. RFID Panel
In the head there contains:
1. The Video Transmission Module (VTM)
2. Speed Monitor Module (SMM)

These components interact with the subsystems to ensure the rules are always being followed.
The PMM interacts will all components as interfaces between the battery and everything else. The battery plugs in through an xt60 connector. There are four lines of power that go out of the PMM (each of the systems mentioned before.) These go to the bottom slipring breakout board. The PMM will also connect to the rest of the referee system through aviator cables. These aviator cables must be connected in a daisy chain. The armor panels are specifically connected via 6-pin connectors, which are also connected in a daisy chain. The referee components in the head are wired the same way. 

CAN Protocol\
CAN stands for Controller Area Network. It is a protocol to transmit data through measuring the voltage difference between two wires. These two wires are known as CAN high and CAN low. If noise occurs in the system both CAN high and CAN low are affected equally and the difference in voltage is maintained. 
