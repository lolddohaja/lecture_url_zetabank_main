Code Explanation
==================

With our follow along examples, we were able to move our robot arm with precision as well as produce music with our 
integrated speaker within the zetabot. The instructional codes have been compile into a jupyter notebook for the 
ease of use. 
This section will explain the libraries used for the *follow along* section. 


Sound
-------------------------------

For our dancing robot demonstration, we published an array of integer to ROS Topic called ``/robot_sound``. 

The ``robot_sound`` topic recieves integer array of size 3: ``[slot1, slot2, slot3]``.

- **slot1**: Recieves binary integer (1, 0) dictating whether to play the sound (1) or stop the sound (0).
- **slot2**: File ID (ranges from 0 ~ 9).
- **slot3**: Directory ID. (set to 1)