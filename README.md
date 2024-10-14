# Dungeon Crawler 1D

## Description
An Arduino-based, 1D, LED-loving dungeon crawler. This project is forked from [CRITTERS/TWANG](https://github.com/Critters/TWANG) and inspired by Line Wobbler by Robin B. It uses an LED strip to create an immersive dungeon crawler-style experience where players navigate through various levels, avoiding enemies and obstacles.

## Features
- Multiple game levels with increasing difficulty
- Player movement controlled by an MPU6050 accelerometer
- Enemy AI with different movement patterns
- Lava and conveyor belt obstacles
- Boss battles
- Lives system with LED indicators
- Sound effects using toneAC library
- Particle effects for player death
- Screensaver mode

## Hardware Requirements
- Arduino board (compatible with FastLED and I2Cdev libraries)
- LED strip (WS2812B or similar, compatible with FastLED)
- MPU6050 accelerometer
- Speaker for sound effects
- 3 LEDs for life indicators

## Software Dependencies
- FastLED library
- I2Cdev library
- MPU6050 library
- Wire library
- toneAC library
- iSin library
- RunningMedian library

## Setup
1. Connect the LED strip to the specified data pin (default: 3)
2. Connect the MPU6050 to the I2C pins of your Arduino
3. Connect a speaker to the appropriate pin for toneAC
4. Connect 3 LEDs to pins 30, 32, and 34 for life indicators
5. Upload the code to your Arduino

## Gameplay
- Tilt the MPU6050 to move the player (green LED) left or right
- Avoid red enemy LEDs and lava (orange LEDs)
- Reach the blue exit LED to complete a level
- Shake the MPU6050 to perform an attack
- Defeat the boss (dark red LEDs) in the final level

## Customization

### Joystick Smoothening
The game includes several parameters to adjust the responsiveness and smoothness of the joystick (accelerometer) control. These can be found in the code and include:

- LOWPASS_ALPHA: Adjusts the smoothing effect (lower values = more smooth)
- JOYSTICK_DEADZONE: Defines the threshold for ignoring small movements
- MEDIAN_SAMPLE_SIZE: Sets the number of samples used for smoothing
- ACCEL_SCALE_FACTOR: Scales the accelerometer readings
- MOVE_SPEED_FACTOR: Adjusts how quickly the player moves based on joystick tilt

You can experiment with these values to find the best balance between responsiveness and smooth control for your specific hardware setup.

### Modifying / Creating Levels
Find the loadLevel() function in the code. It contains a switch statement with 10 predefined levels. You can modify existing levels or add new ones using the following functions:

1. Set player start position:
   playerPosition; Where the player starts on the 0 to 1000 line. If not set it defaults to 0.

2. Spawn an enemy:
   spawnEnemy(position, direction, speed, wobble);
   - position: 0 to 1000
   - direction: 0/1, initial direction of travel
   - speed: >=0, speed of the enemy (recommended between 1 and 4)
   - wobble: 0=regular moving enemy, 1=sine wave enemy (speed sets wave width)

3. Create a spawn pool (continuously spawning enemies):
   spawnPool[poolNumber].Spawn(position, rate, speed, direction);
   - position: 0 to 1000
   - rate: milliseconds between spawns
   - speed: speed of spawned enemies
   - direction: 0=towards start, 1=away from start

4. Add lava:
   spawnLava(startPoint, endPoint, ontime, offtime, offset);
   - startPoint, endPoint: 0 to 1000
   - ontime: How long (ms) the lava is ON for
   - offtime: How long (ms) the lava is OFF for
   - offset: Delay (ms) before lava activates

5. Add a conveyor belt:
   spawnConveyor(startPoint, endPoint, direction);
   - startPoint, endPoint: 0 to 1000
   - direction: the direction of travel 0/1

6. Spawn a boss:
   spawnBoss()
   - No parameters (always spawns in the same place with 3 lives)
   - Modify Boss.h to change boss behavior

## License
This project is released under the MIT License.

## Acknowledgements
- Original CRITTERS/TWANG project
- Line Wobbler by Robin B
- FastLED, I2Cdev, and other open-source libraries used in this project
