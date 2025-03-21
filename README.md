# scaffold-2
This interactive artwork explores the concept of emotions as masks. The installation consists of four Japanese-inspired masks, each representing a distinct emotion, mounted on a rotating disc. These masks continuously circle around, symbolizing the way emotions shift and change over time. 
from machine import Pin, PWM
import time
import _thread

# Stepper Motor Control Pins
coil_A = Pin(21, Pin.OUT)
coil_B = Pin(18, Pin.OUT)
coil_C = Pin(19, Pin.OUT)
coil_D = Pin(22, Pin.OUT)

# Optimized Step Delay
STEP_DELAY = 0.001 # Adjust this if too fast or too slow

# Stepper Motor Sequence for Smooth Rotation
sequence = [
 (1, 0, 0, 1),
 (1, 1, 0, 0),
 (0, 1, 1, 0),
 (0, 0, 1, 1)
]

# Function to run stepper motor at high speed
def stepper_motor():
 while True:
 for step in sequence:
 coil_A.value(step[0])
 coil_B.value(step[1])
 coil_C.value(step[2])
 coil_D.value(step[3])
 time.sleep(STEP_DELAY) # Adjust for speed

# Servo Motor Setup
servo_motor = PWM(Pin(4))
servo_motor.freq(50)

# Function to move servo quickly
def move_servo():
 while True:
 servo_motor.duty(30) # 0-degree position
 time.sleep(0.01) # Faster switching
 servo_motor.duty(120) # 90-degree position
 time.sleep(0.01)

# Run both motors simultaneously
_thread.start_new_thread(stepper_motor, ())
move_servo()
