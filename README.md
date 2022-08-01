# Third-task

Brogramming arm for robot

Quick Start

$ sudo apt-get install ros-kinetic-simple-arm

Launch:

$ roslaunch simple_arm simple_arm.launch joystick_serial_dev:=/dev/input/js0 microcontroller_serial_dev:=/dev/ttyACM0

Nodes

Serial data packet:

(FLOAT) GRIP,

(FLOAT) WRIST_ROLL,

(FLOAT) WRIST_PITCH,

(FLOAT) UPPER_ELBOW,

(FLOAT) LOWER_ELBOW,

(FLOAT) BASE_YAW,

(FLOAT) CAMERA

Install PlatformIO

$ sudo python -c "$(curl -fsSL https://raw.githubusercontent.com/platformio/platformio/master/scripts/get-platformio.py)"

# Enable Access to Serial Ports (USB/UART)

$ sudo usermod -a -G dialout <your username here>

$ curl https://raw.githubusercontent.com/platformio/platformio/develop/scripts/99-platformio-udev.rules  > /etc/udev/rules.d/99-platformio-udev.rules

# After this file is installed, physically unplug and reconnect your board.

$ sudo service udev restart

Create a PlatformIO project

$ roscd simple_arm

$ cd ./arm_firmware/

# Find the microcontroller that you have in the list of PlatformIO boards

$ pio boards | grep -i mega2560

# Use the name of your board to initialize your project

$ pio init --board megaatmega2560

Modify wiring if necessary

$ vim src/main.cpp +9

Depending on how you want to wire your microcontroller this wiring can be changed:

   1 struct JOINTPINS{
   
   2   int wrist_roll = 9; // wrist roll pin
   
   3   int wrist_pitch = 10; // wrist pitch pin
   
   4   int upper_elbow = 11; // upper elbow pin
   
   5   int lower_elbow = 12;  // lower elbow pin
   
   6   int base_yaw = 13;  // base yaw pin
   
   7   int grip_enable = A4;  // gripper enable pin
   
   8   int grip_open = A5;  // gripper open pin
   
   9   int grip_close = A6;  // gripper close pin
   
  10   int cam_tilt = 7; // camera servo pin
  
  11 }pins;

Modify PWM Settings

$ vim src/main.cpp +4

Edit the following section to match your motor controller PWM specs:

   1 // PWM specs of the Victor SP motor controller.
   
   2 //https://www.vexrobotics.com/217-9090.html
   
   3 #define sparkMax 650 // Full-reverse input pulse
   
   4 #define sparkMin 2350 // Full-forward input pulse

Deploy Code to Arduino

$ pio run --target upload











