Code Explanation
==================

Teaching the Robot Arm
----------------------------------------

-   Since manually instructing angle information for each of the servo for every movement is difficult, you may 
    teach you robot arm moves. 
    
    -   By default, the servos are in locked position. The function that is responsible for locking and unlocking the robot arm is ``Arm_Button_Mode(mode)`` function

        The function recieves 1 input *mode* from the user. The mode must be an binary integer of either 1 and 0.
        
        1.  ``mode=0``: All servos are locked (default)
        2.  ``mode=1``: All servos are released 

    -   To learn a movement, ``Arm_Action_Study()`` function is used. To study a movement, simply activate the function and move the arm
        If you wish to have multiple movements, after completing one movement, activate the function again and repeat the process. 
        *(NOTE!)* The after activating the function, only the first movement of the robot is registered. If it is a chain movement, please activate the function at the start of each movement. 
        After finishing the movement put the robot arm back to the locked mode. ``Arm_Button_Mode(0)``

    -   To see the number of learned movements, run ``Arm_Read_Action_Num()`` function which will return the total learned movements.
    -   To execute the learned movements, run ``Arm_Action_Mode(mode)`` function. This function will sequentially run all the learned movements from the first to last. 
        We can have 3 different execution mode: 

        1.  ``mode = 1``: Execute all the sequence only once.
        2.  ``mode = 2``: Execute all the sequence repeatedly.
        3.  ``mode = 3``: Stop the sequence. 

    -   To clear all the previously learned movements, run ``Arm_Clear_Action()`` function. 