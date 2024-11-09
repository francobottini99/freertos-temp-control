# Temperature Measurement System Implemented in Real-Time Operating System

Application of a real-time operating system in an embedded system. Simulation of a temperature control system with a low-pass filter. UART communication with a computer to view the system's status and change the filtering coefficient.

The embedded system used is a *Stellaris LM3S811* microcontroller. The operating system used is FreeRTOS. The system was tested through the QEMU simulation tool. The port to the real board was not done.

### Authors:
- **Bottini, Franco Nicolas**

### How to Clone?

To compile the project, once the repository is cloned, simply run the `make` command in the root folder of the project.

```bash
$ git clone https://github.com/francobottini99/SIS-TEMPRTOS-2024.git
$ cd SIS-TEMPRTOS-2024
$ make
```

## Summary

The embedded system has five tasks: a temperature reading task, a temperature filtering task, a task for plotting the temperature, a task for displaying the system status, and a task for receiving commands via UART.

The communication between the temperature reading and filtering tasks, and the filtering and plotting tasks is done via message queues.

The priority of the tasks was adjusted so that the temperature reading task has the highest priority, followed by the temperature filtering task, the temperature plotting task, the system status display task, and finally the UART command receiving task.

A *stack* was assigned to each task based on the estimated memory usage for each, with an added safety margin.

## Execution

To run the program using QEMU, an execution script `emulate.sh` is provided.

```bash
$ ./emulate.sh
```

If you wish to modify the default filtering coefficient with which the program runs, you can execute the script with the desired value as an argument.

```bash
$ ./emulate.sh 15 # Filtering coefficient = 15
```

> [!WARNING]
> The filtering coefficient must be an integer greater than 0. By default, the filtering coefficient is 5. If an invalid value is entered, the default value will be used.

> [!NOTE]
> QEMU must be installed to run the script.

## Visualization

When the program is executed, a QEMU window will open with the simulation of the embedded system. In the QEMU window, you can view the resulting graph from the temperature simulation and filtering process.

<p align="center">
  <img src="Imgs/Graph.png" alt="Graph">
</p>

Additionally, the system's status is printed in the terminal. You can see the CPU load, available *stack*, and the number of *ticks* occupied by each task in execution.

<p align="center">
  <img src="Imgs/Stats.png" alt="Stats">
</p>

> [!NOTE]
> The simulated temperature sensor frequency is 10 Hz, while the information is displayed in the terminal at a frequency of 0.5 Hz.
