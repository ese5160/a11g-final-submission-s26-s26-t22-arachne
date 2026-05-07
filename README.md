[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/Y5lYn2wb)

# a11g-final-submission

**Team Number: 22**

**Team Name: Arachne**

| Team Member Name | Email Address          | GitHub Username |
| ---------------- | ---------------------- | --------------- |
| Amehja Williams  | amehjaw@seas.upenn.edu | prm2023         |
| Lubha Churiwala  | lubha@seas.upenn.edu   | LubhaC          |

**GitHub Repository URL: https://github.com/ese5160/a11g-final-submission-s26-s26-t22-arachne.git**

## 1. Video Presentation: [https://drive.google.com/file/d/1NOnBmTIpOmjb-eG-j_7bhOsVzotfvLr7/view?usp=sharing](https://drive.google.com/file/d/1NOnBmTIpOmjb-eG-j_7bhOsVzotfvLr7/view?usp=sharing)

## 2. Project Summary:

* **Device Description**

  * Our Project: Arachne: The Smart Money Monitoring System
  * Inspiration: Building financial savviness at any age.
  * Problem: There are plenty of apps that help kids and adults alike manage their money, but we wanted to integrate an interactive physical system that builds good savings habits.
  * How do you use the Internet to augment your device functionality?: Towards this end, the IoT aspect of our project was critical for encouraging financial awareness, both when users are at home with the piggy bank and when they are away. The IoT-augmented mobile application allows users to track their savings habits and bank balance on-the-go.
* **Device Functionality**

  * Explain how your Internet-connected device is designed: The core of our  IoT device design is the integration of four break-beam IR sensors, one for each denomination of coin (nickel, quarter, penny, and dime). When an emitter-receiver pair is broken, that sensor triggers a deposit event.
  * ![1778125719013](image/README/1778125719013.png)
* **System Block Diagram:**

  ![1778125747232](image/README/1778125747232.png)
* **Challenges**

  * Where did you face difficulties? How did you solve them? This could be in firmware, hardware, software, integration, etc.:

    ![1778125774394](image/README/1778125774394.png)

    * Our firmware challenges revolved around troubleshooting issues with the motors, over-the-air-firmware-update, and the LCD SPI configuration. The PWM commands we were sending the motors built without errors. However, when the event triggered motor rotation, they stalled.
      * Solution: We surmised that the PCB power architecture did not provide enough current to the motors for the 360 degree rotation. Thus, we attempted to power the motors externally but observed the same stalled behavior.
    * Our integration challenges primarily dealt with needing to power both the motors (see above) and soundboard externally.  The soundboard draws 3A of current whereas our PCB supplies a max of 2A.
      * Solution: We utilized the DC power supply to provide power for both the soundboard and motors during debugging.
    * The hardware integration challenges we faced involved a) the J2 (battery) connector and b) the PSRAM pins on the MCU. The J2 connector was unfortunately ripped off when we attempted to unplug the battery from the PCB during debugging. The GPIO pins we routed to the soundboard header during the PCB design stage turned out to be PSRAM pins, which are reserved for MCU usage.
      * Solution A: We soldered a new connector. Although the connector had successfully powered the board and all brung-up peripherals before being ripped off, it no longer functioned when a new connector was soldered. Thus, we surmised there was damage to the pads.
      * Solution B: Since motor bring-up was unsuccessful, we decided to utilize one of those GPIO pins (GPIO_10) as well as the extra UART (TX,RX) pins we had routed as a backup usage mode for the soundboard.
* **Prototype Learnings**

  ![1778125798123](image/README/1778125798123.png)

  * What lessons did you learn by building and testing this prototype?
    * Measure Twice, Cut Once: The routing of the PSRAM pins could have been avoided with more insight from the datasheet. Next time, we would go over our entire pin assignment diagram using the Pin Tool in simplicity studio and make sure we are not utilizing reserved pins.
    * Tiered testing: We learned how useful both devboards and breadboards can be for isolating issues with peripherals. We were very grateful to be able to use the devboard to test our soundboard and speaker to ensure proper functionality before integration. We also learned how to isolate firmware problems and developed an effective debugging checklist (i.e. first checking power and connections, continuity testing with the multimeter, then correct firmware version, cloud connectivity, etc.)?
  * What would you do differently if you had to build this device again?
    * Component Selection: We would be more cognizant of our design decisions for component selection. The soundboard requires 3A of current alone, so we would have selected a less power-hungry board. Nevertheless, it was a very successful peripheral because of prior experience with this component, though it came at the cost of more power.
* **Next Steps & Takeaways**

  ![1778125815244](image/README/1778125815244.png)

  * What steps are needed to finish or improve this project?

    * We would like to bring up our 2nd PCBA and validate the battery validation so that all debugging starts and ends with the battery being plugged in. Initially, we had done all debugging with USB power and then attempted to shift to battery power only. We could then troubleshoot the motor separately and expand the alarm features so that users can set multiple alarm sounds if they so choose.
  * What did you learn in ESE5160 through the lectures, assignments, and this course-long prototyping project?

    * RTOS task scheduling and the bootloader quiz were essential in understanding the key turning points of our project.
* **Project Links**

  * Provide a URL to your Node-RED instance for our review (make sure it’s running on your Azure instance!):
    * Dashboard: [http://52.159.83.167:1880/dashboard/](http://52.159.83.167:1880/dashboard/)
    * Instance: [http://52.159.83.167:1880/](http://52.159.83.167:1880/)
  * Provide the share link to your final PCBA on Altium 365.: [https://upenn-eselabs.365.altium.com/designs/50E9F919-A841-4818-932F-F08D4C5303F6](https://upenn-eselabs.365.altium.com/designs/50E9F919-A841-4818-932F-F08D4C5303F6)

## 3. Hardware & Software Requirements

## 4. Project Photos & Screenshots

1. Casework

   ![1778123212804](image/README/1778123212804.png)

   <img src="image/README/1778122661517.png" width="30%"></img> <img src="image/README/1778122679515.png" width="30%"></img> <img src="image/README/1778122692246.png" width="30%"></img> <img src="image/README/1778122729341.png" width="30%"></img> <img src="image/README/1778122821207.png" width="30%"></img>

   ![1778123240937](image/README/1778123240937.png)
2. The standalone PCBA, top

   ![1778123358220](image/README/1778123358220.png)
3. The standalone PCBA, bottom

   ![1778123377064](image/README/1778123377064.png)
4. Thermal camera image while the board is running under load

   ![1778123433674](image/README/1778123433674.png)
5. The Altium Board design in 2D view (screenshot)
6. The Altium Board design in 3D view (screenshot)
7. Node-RED dashboard (screenshot)
8. Node-RED backend (screenshot)
9. Block diagram of your system (You may need to update this to reflect changes throughout the semester.)

## 5. Codebase

Do *not* commit any of your source code to this repository. Rather, provide links to the other GitHub repository you've already been using with your firmware.

- A link to your final embedded C firmware codebases: https://github.com/ese5160/final-project-firmware-s26-t22-arachne-1/tree/main/customPCB_WorkingCode/ir/ir
- A link to your Node-RED dashboard code: https://github.com/ese5160/final-project-firmware-s26-t22-arachne-1/tree/main/NodeRed
- Links to any other software required for the functionality of your device
