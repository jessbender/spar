import rospy
from std_msgs.msg import UInt8
from gpiozero import Servo
from time import sleep

# Servo parameters
SERVO_PIN = 21
servo = Servo(SERVO_PIN)

def callback(msg):
    # payload commands message structure:
    # both close:   0b00000000 (0)
    # both open:    0b00000011 (3)
    # tracker open: 0b00000010 (2)
    # epi open:     0b00000001 (1)
    
    if msg.data == 0 or msg.data == 1:
        servo.min()
        sleep(2)
    elif msg.data == 3 or msg.data == 2:
        servo.max()
        sleep(0.5)
    else:
        rospy.logwarn("Received invalid command!")

def main():
    # Initialize ROS node
    rospy.init_node('servo_controller_node')
    
    # Subscribe to payloadcommands topic
    rospy.Subscriber('payloadcommands', UInt8, callback)
    
    # Keep the node alive
    rospy.spin()

if __name__ == '__main__':
    main()