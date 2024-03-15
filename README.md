import RPi.GPIO as GPIO
import time

# Set the GPIO mode to BCM
GPIO.setmode(GPIO.BCM)

# Define the GPIO pins for the motors
motor1_pin1 = 2
motor1_pin2 = 3
motor2_pin1 = 4
motor2_pin2 = 17

# Set the pins as output
GPIO.setup(motor1_pin1, GPIO.OUT)
GPIO.setup(motor1_pin2, GPIO.OUT)
GPIO.setup(motor2_pin1, GPIO.OUT)
GPIO.setup(motor2_pin2, GPIO.OUT)

# Function to move the car forward
def forward():
    GPIO.output(motor1_pin1, GPIO.HIGH)
    GPIO.output(motor1_pin2, GPIO.LOW)
    GPIO.output(motor2_pin1, GPIO.HIGH)
    GPIO.output(motor2_pin2, GPIO.LOW)

# Function to move the car backward
def backward():
    GPIO.output(motor1_pin1, GPIO.LOW)
    GPIO.output(motor1_pin2, GPIO.HIGH)
    GPIO.output(motor2_pin1, GPIO.LOW)
    GPIO.output(motor2_pin2, GPIO.HIGH)

# Function to stop the car
def stop():
    GPIO.output(motor1_pin1, GPIO.LOW)
    GPIO.output(motor1_pin2, GPIO.LOW)
    GPIO.output(motor2_pin1, GPIO.LOW)
    GPIO.output(motor2_pin2, GPIO.LOW)

# Clean up GPIO on exit
def cleanup():
    GPIO.cleanup()

try:
    while True:
        action = input("Enter action (f: forward, b: backward, s: stop, q: quit): ")

        if action == 'f':
            forward()
        elif action == 'b':
            backward()
        elif action == 's':
            stop()
        elif action == 'q':
            break

except KeyboardInterrupt:
    pass

finally:
    cleanup()
