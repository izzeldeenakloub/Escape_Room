# Escape Room - Digital Fort

## Overview

**Escape Room - Digital Fort** is an embedded systems project that simulates a digital escape-room game using the **PIC16F877A microcontroller**. The player must complete three sequential challenges to escape the room. Each challenge uses different embedded system concepts such as digital input/output, ADC conversion, LCD interfacing, 7-segment display control, timers, LEDs, push buttons, and buzzer feedback.

The project was developed for the **Embedded Systems Lab** and simulated using **Proteus**. The main implementation was written in **PIC Assembly**, with an additional Embedded C version included for comparison or bonus implementation.

## Project Idea

The system represents a locked digital room. To escape, the player must solve three challenges in order:

1. Prime number challenge
2. ADC range detection challenge
3. Timed math challenge

If the player solves all challenges correctly, the system displays a winning message and activates the output indicators. If the player fails any challenge, the game resets back to the first challenge and displays a failure message.

## Features

* PIC16F877A-based embedded game
* Three sequential logic challenges
* Digital input using switches and push buttons
* Analog input using a potentiometer and ADC
* LCD display for messages and instructions
* 7-segment display for numeric output and countdown
* LED feedback for correct/incorrect states
* Buzzer activation on winning condition
* Reset logic after failure
* Proteus simulation support
* Assembly and Embedded C source files

## System Challenges

### Challenge 1: Prime Number Check

In the first challenge, the player enters a 4-bit number using switches.

The system checks whether the entered number is prime by comparing it with a predefined list of small prime numbers.

If the number is prime:

* A green LED turns ON
* A value is displayed on the 7-segment display
* The player proceeds to the next challenge

If the number is not prime:

* The game resets
* The LCD displays a failure message

### Challenge 2: ADC Range Detection

In the second challenge, the player rotates a potentiometer.

The PIC16F877A reads the analog voltage using its internal ADC module. The system then checks whether the ADC value falls inside the required range.

Possible responses:

* If the value is in the correct range, the LCD displays `You are correct`
* If the value is close to the correct range, the LCD displays `You are so close`
* If the value is wrong, the system does not accept the answer

This challenge demonstrates ADC configuration, analog signal reading, and range-based decision making.

### Challenge 3: Timed Math Challenge

In the final challenge, the player presses a Start button to begin a random math problem.

The system displays the problem on the LCD and starts a countdown from 9 using the 7-segment display.

The player must:

1. Read the math problem
2. Enter the answer using switches
3. Press the Finish button before the timer reaches zero

If the answer is correct before timeout:

* The LCD displays `YOU WIN! Escape`
* All LEDs are activated
* The buzzer turns ON

If the answer is wrong or time runs out:

* The LCD displays `Hard Luck`
* The game resets to Challenge 1

## Hardware Components

The project uses the following components:

* PIC16F877A microcontroller
* 4-bit input switches
* Start and Finish push buttons
* Potentiometer for analog input
* 16x2 LCD display
* 7-segment display
* LEDs
* Buzzer
* Proteus simulation environment

## Microcontroller

The project is built around the **PIC16F877A** microcontroller.

The PIC16F877A was used because it supports:

* Digital input/output ports
* ADC module
* Timers
* Interrupts
* LCD and display interfacing
* Low-level embedded control

## Input Devices

### Switches

The switches are used to input binary values into the system.

They are used mainly in:

* Prime number challenge
* Math answer input

### Push Buttons

Push buttons are used for control actions such as:

* Starting the math challenge
* Submitting the answer
* Moving between challenge states

### Potentiometer

The potentiometer is used as an analog input source for the ADC challenge.

By rotating the potentiometer, the player changes the analog voltage read by the PIC.

## Output Devices

### LCD Display

The LCD is used to show:

* Challenge messages
* Feedback messages
* Math problems
* Winning or losing messages

### 7-Segment Display

The 7-segment display is used to show:

* Challenge output values
* Countdown timer during the math challenge

### LEDs

LEDs are used as visual indicators for:

* Correct challenge completion
* System state feedback
* Winning condition

### Buzzer

The buzzer is activated when the player successfully completes all challenges and escapes the digital room.

## Software Design

The program is structured as a state-based embedded system.

Each challenge represents a different state:

```text
Start
  |
  v
Challenge 1: Prime Number Check
  |
  v
Challenge 2: ADC Range Detection
  |
  v
Challenge 3: Timed Math Challenge
  |
  v
Win State
```

If the player fails at any stage, the system returns to the first challenge.

```text
Failure
  |
  v
Reset to Challenge 1
```

## Program Flow

```text
Initialize system
  |
  v
Configure ports, ADC, LCD, 7-segment display, LEDs, and buttons
  |
  v
Wait for player input
  |
  v
Run prime number challenge
  |
  v
If correct, continue to ADC challenge
  |
  v
Read analog value from potentiometer
  |
  v
Check ADC range
  |
  v
If correct, continue to math challenge
  |
  v
Display math problem and start countdown
  |
  v
Check answer before timeout
  |
  v
If correct, display win message and activate LEDs/buzzer
  |
  v
If wrong or timeout, display Hard Luck and reset
```

## Tools Used

* **MPLAB**
* **Proteus**
* **PIC16F877A**
* **PIC Assembly**
* **Embedded C**

## Repository Structure

```text
Escape-Room-Digital-Fort/
│
├── New Project.pdsprj   # Proteus simulation project
├── src_asm.asm               # PIC Assembly source code
├── src_C.c                # Embedded C implementation
├── projectReport.pdf               # Project report
└── README.md                       # Project documentation
```

## How to Run the Project

### 1. Open the Source Code

Open the Assembly or C source file in MPLAB.

For Assembly:

```text
src_asm.asm
```

For Embedded C:

```text
src_C.c
```

### 2. Build the Project

Compile the code in MPLAB to generate the HEX file.

The HEX file is the compiled program that will be loaded into the PIC16F877A microcontroller in Proteus.

### 3. Open the Proteus Simulation

Open the Proteus project file:

```text
EscapeRoom_DigitalFort.pdsprj
```

### 4. Load the HEX File

Double-click the PIC16F877A microcontroller in Proteus.

Then load the generated HEX file into the microcontroller.

### 5. Run the Simulation

Start the Proteus simulation.

Use the switches, buttons, and potentiometer to interact with the game.

## Testing

The system was tested in Proteus by checking each challenge individually and then testing the full game sequence.

### Test Cases

| Challenge      | Input                          | Expected Output               |
| -------------- | ------------------------------ | ----------------------------- |
| Prime Check    | Prime number such as 5         | LED ON and 7-segment output   |
| Prime Check    | Non-prime number such as 6     | Game resets                   |
| ADC Range      | Potentiometer in correct range | LCD displays correct message  |
| ADC Range      | Potentiometer near range       | LCD displays close message    |
| Math Challenge | Correct answer before timeout  | Win message, LEDs, and buzzer |
| Math Challenge | Wrong answer or timeout        | Hard Luck message and reset   |

## Main Challenges

Some of the main development challenges were:

* Implementing reliable delay logic
* Handling push-button inputs
* Configuring ADC correctly
* Displaying messages on the LCD
* Controlling the 7-segment display
* Coordinating multiple outputs in the same system
* Managing the game flow between different challenges
* Keeping the system logic organized in low-level embedded code

## What I Learned

This project helped strengthen practical embedded systems skills, including:

* PIC16F877A programming
* Assembly language programming
* Embedded C programming
* Digital input/output handling
* ADC reading and analog signal processing
* LCD interfacing
* 7-segment display control
* Button handling and delays
* Proteus simulation
* Embedded game logic
* System integration and debugging

## Possible Future Improvements

The project can be improved by adding:

* More challenge levels
* Difficulty selection
* Better random math problem generation
* Score tracking
* Sound effects using the buzzer
* LCD menu system
* EEPROM storage for high scores
* Real hardware implementation
* Improved button debouncing
* Timer interrupt-based countdown

## Authors

* Izzeldeen Akloub
* Mohammad Alghananim
* Marlo Rizkallah
* Heyam Dababat

## Project Contribution

My contribution focused on:

* Prime number logic
* 7-segment display implementation
* Testing and debugging related challenge behavior

## License

This project is intended for educational purposes.
