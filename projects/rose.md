---
layout: project
type: project
image: img/rose/Roselogo.png
title: "VIP Team RoSE"
date: 2024-Present
published: true
labels:
  - Robotic Operating System (ROS2)
  - GitHub
  - Python
summary: "Team RoSE is a multidisciplinary student group at UH Mānoa that designs and builds simulated Mars rovers to compete in the  University Rover Challenge (URC)."
---
## Overview
Team Robotic Space Exploration (RoSE) is a multidisciplinary undergraduate project team at UH Mānoa, bringing together students from engineering, astrobiology, computer science, and related fields. As part of the Vertically Integrated Projects (VIP) program, Team RoSE designs and builds advanced robotic systems to compete in the University Rover Challenge (URC). At the 2025 URC competition, team RoSE placed **24th** out of 114 international teams. URC is an international competition focused on building simulated Mars Rovers that compete in the following 4 missions:

#### Science Mission
Teams navigate to candidate sites (within ~0.5 km of the command station), document each site with panoramas and close-ups (including scale and cardinal directions), record GNSS coordinates, and build a stratigraphic profile. The rover performs on-board analyses with at least one life-detection method plus a second science capability, measures subsurface temperature and soil moisture (~10 cm depth), then collects a ≥5 g sample from ≥10 cm below the surface, seals it in a cache, and returns it to the judges for debrief. Afterwards, teams will present their finds and analysis of the site to the judges. A written science plan is also required and factors into scoring. 

#### Delivery Mission
A staged, timed obstacle course (total ~30–60 min) where the rover traverses increasingly difficult terrain that can be beyond line of sight. It must follow marked paths, open boxes, pick up and deliver objects, read signs, and locate equipment in large search areas. For 2025, teams may optionally deploy a drone to help scout, read signage, relay radio, or search. It’s not required but can assist at each stage. Points are awarded per task and stage. 

#### Equipment Servicing Mission
 After a short drive (~0.25 km) to a mock lander, the rover performs dexterous arm tasks in any order within 30 min, including: deliver the cached science sample to a drawer on the lander, unlatch/open panels, push buttons/flip switches/turn knobs, operate a 4-position joystick while watching a gauge, remove/insert a rugged USB stick, and complete an autonomous typing task by entering a provided launch key on a vertical keyboard. 

 <figure class="centered">
  <img src="{{ '/img/rose/mock_lander.png' | relative_url }}">
  <figcaption>Rover attempting to flip a switch using robotic arm</figcaption>
</figure>

#### Autonomous Navigation Mission
In 30 min and ≤~2 km total travel, the rover must autonomously reach: two GNSS-only points (stop within ~3 m), three posts marked with ARUCO tags (stop within ~2 m), and two objects on the ground (e.g., an orange rubber mallet and a 1 L bottle; stop within ~2 m), sometimes with obstacle avoidance. The rover signals mode/status via a rear LED (red = autonomous, blue = teleop, flashing green = arrival). Operators can abort and command an autonomous return or have a teleoperated return with a points penalty. 

### What I Contributed
My primary contribution to Team RoSE was developing the teleoperation system for the rover’s 5-degree-of-freedom robotic arm. I accomplished this by writing a custom ROS 2 node that handled serial communication between the operator’s controller and the rover. The node translated joystick inputs into byte-encoded commands, which were transmitted over a serial link to an Arduino microcontroller. The Arduino then decoded the bytes and sent appropriate signals to the motor controllers, allowing each joint of the robotic arm to move precisely in response to operator input. This system enabled the rover to pick up, manipulate, and place objects during competition tasks.

### What I Learned
From this experience, I gained a much deeper understanding of the interaction between high-level software (ROS 2 nodes) and low-level embedded systems (Arduino microcontrollers and motor controllers). I learned how to design an efficient communication protocol, debug serial links, and validate that the control pipeline remained responsive under real operating conditions. Beyond the technical skills, I also learned how important modular design and clear documentation are in a large multidisciplinary project. This was especially apparent when multiple subsystems, like arm control, drive, and science payload, must integrate seamlessly for the rover to succeed.

