Code Explanation
==================

Robot arm Movements
--------------------

-   In order to instruct the robot arm, we must first initialize it as an object.

    .. code-block:: python

        # Register robot arm as an object
        Arm = Arm_Device()
        time.sleep(.1)
    
    As you may have noticed, we after the arm is initialized as an object, we pause our program 
    for one tenth of a second. We will regularly follow this protocol when we are giving the 
    robot arm multiple instructions at the same time. We do not want some of the instructions cutting
    in while other insturctional movements have not finished. 


Basic Movements
--------------------

-   For basic movements, we use ``Arm_serial_servo_write(servo_id, angle, time)`` function. The function can accept 3 parameters
    from the user.

    1. servo_id: The servo_id represents the motors responsible for the robot arm movements. There are total of 6 robots, from the bottom most motor responsbile for rotational movement and to the last motor which is responsible for the pincher
    2. angle: The angle determines how much the motor should move from its current position. 
    3. time: The time in which the movement is to be conducted. (in 1/2 mili seconds)

    .. code-block:: python

        Arm = Arm_Device()
        # Move the 6th servo (which is the pincher) to 90 degree angle for 2 second. 
        Arm.Arm_serial_servo_write(6, 90, 1000)
        time.sleep(.1)
    
-   You may also move multiple servo's at the same time using ``Arm_seria_servo_write6(...params)``` function.
    The function recieves angle information for all the servor and the required time for movement completion. 

    .. code-block:: python

        # Move all the servo's 90 degrees for 2 second
        Arm.Arm_serial_servo_write6(90, 90, 90, 90, 90, 90, 1000)

    You may give the same instructions in a list format using ``Arm_seria_servo_write6_array(array, time)`` function. 

Reading the Current Angle of the Servo
----------------------------------------

-   All the servos at any given moment are rotated to a specific angle. 
    In order to determine the current angle of the motors, we may run ``Arm_serial_servo_read(servo_id)``` function.

    -   By specifying the desired servo number, we may get the current angle information of the specified servo. 
    
    .. code-block:: python

        servo_angle = Arm.Arm_serial_servo_read(servo_id)