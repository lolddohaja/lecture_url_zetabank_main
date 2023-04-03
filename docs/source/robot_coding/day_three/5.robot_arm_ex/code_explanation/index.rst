Code Explanation
==================

Tacking a Color or a Face
----------------------------------------

-   For tracking tasks, we provide custom library (for color tracking ``color_folow.py`` and ``PID.py``, for face tracking ``dofbot_conf.py``, ``face_follow.py``, ``PID.py``)


Tracking a Color
^^^^^^^^^^^^^^^^^

-   Here are all the libraries used for tracking a color task. 

    -   *cv2*: Computer Vision library
    -   *threading*: Threading library for multi, singular processing.
    -   *random*: Library for generating and controlling random instances.
    -   *time*: Library for time related modules. 
    -   *ipywidgets*: Widget library used to create graphical user interfaces with IPython display.
    -   *IPython.display*: Library with modules that allow for graphical output within jupyter environment
    -   *color_follow*: Custom library with modules that allow for robot arm to follow the color. 

-   Initialization
 

    1.   Create the follow instance for the color_follow modules.
    2.   Initialize model variable with 'General'. Later on it will be changed to whether you wish to learn a new color, learn to track or simply to exit the tracking process.
    3.   Initialize HSV_learning. Later on it will house the learned movement modules. 
    4.   color_hsv: Initialize what red, green, blue, and yellow collow would be (in a spectrum)
    5.   color: Initialize the first color to be random. 

    .. code-block:: python 

        follow = color_follow()
        model = 'General'
        HSV_learning = ()
        color_hsv = {"red": ((0, 25, 90), (10, 255, 255)),
                    "green": ((53, 36, 40), (80, 255, 255)),
                    "blue": ((110, 80, 90), (120, 255, 255)),
                    "yellow": ((25, 20, 55), (50, 255, 255))}

        color = [[random.randint(0, 255) for _ in range(3)] for _ in range(255)]
    
-   Create the widgets for the user, and create a switch variables to change the model. 

    1. Whether to follow the specied color.
    2. Whether to learn a new color.
    3. Whether to learn to follow.
    4. Whether to be in a general mode.
    5. Whether to exit the task. 

-   Main process

    The main function built for our main process is camera function. Within the function:

    1. Initialize the camera input, and the framerate. 

        .. code-block:: python

            # Open camera
            capture = cv.VideoCapture(1)
            capture.set(3, 640)
            capture.set(4, 480)
            capture.set(5, 30)  #set frame

    2. Capture every frame from the camera on loop. Terminate the loop upon closure of the camera.

        .. code-block:: python
            
            while capture.isOpened():
               
        1. Import in the frame of the input feed and resize it to 640, 480 ratio. 

            .. code-block:: python

                _, img = capture.read()

                img = cv.resize(img, (640, 480))

        2. If the model is set to follow the color, activate follow_function and provide the function with the current frame and the color to follow.

            .. code-block:: python

                if model == 'color_follow':
                    img = follow.follow_function(img, color_hsv[choose_color.value])
                    cv.putText(img, choose_color.value, (int(img.shape[0] / 2), 50), cv.FONT_HERSHEY_SIMPLEX, 2, color[random.randint(0, 254)], 2)
            
        3. If the model is set to learn a new color, activate learn function.

            .. code-block:: python

                if model == 'learning_color':
                    img,HSV_learning = follow.get_hsv(img)

        4. If the model is set to learn to follow, activate the learn follow function.

            .. code-block:: python 

                if model == 'learning_follow' :
                    if len(HSV_learning)!=0:
                        print(HSV_learning)
                        img = follow.learning_follow(img, HSV_learning)

                        cv.putText(img,'LeColor', (240, 50), cv.FONT_HERSHEY_SIMPLEX, 1, color[random.randint(0, 254)], 1)
        
        5. If the model is set to exit, close all the windows opened and release the camera.

            .. code-block:: python 

                if model == 'Exit':
                    cv.destroyAllWindows()
                    capture.release()
                    break
    
    3. To activate the function above, first activate a display output, then within a thread run the function.

        .. code-block:: python

            display(controls_box,output)
            threading.Thread(target=camera, ).start()


Tracking a Face
^^^^^^^^^^^^^^^^

The steps taken for tracking a face is very similar to tracking a color. We use an cascading calssifier, an ensemble learning 
model based on the concatenation of several classifiers. We will be using a pretrained xml model named ``haarcascade_frontalface_default.xml``
with our OpenCV function. 

Our tracking model does not involve re-training with new data, hence, we do not need many different model options 
similar to the *Tracking a Color* task. 

-   Here are all the libraries used for tracking a color task. 

    -   *cv2*: Computer Vision library
    -   *threading*: Threading library for multi, singular processing.
    -   *time*: Library for time related modules. 
    -   *ipywidgets*: Widget library used to create graphical user interfaces with IPython display.
    -   *IPython.display*: Library with modules that allow for graphical output within jupyter environment
    -   *face_follow*: Custom library with modules that allow for robot arm to follow the face. 

-   First initialize the robot arm position as well as creating the instances for the face follow model and the mode for the model.

    .. code-block:: python

        import Arm_Lib
        Arm = Arm_Lib.Arm_Device()
        joints_0 = [90, 150, 20, 20, 90, 30]
        Arm.Arm_serial_servo_write6_array(joints_0, 1500)

        follow = face_follow()

        model = 'General'

-   Create the controls for the graphical user interface. Unlike the *Follow a Color* task, we do not need 
    many user interfaces, since there is no need to change color or learning a new color. 

    .. code-block:: python 

        button_layout = widgets.Layout(width='250px', height='50px', align_self='center')
        output = widgets.Output()

        exit_button = widgets.Button(description='Exit', button_style='danger', layout=button_layout)

        imgbox = widgets.Image(format='jpg', height=480, width=640, layout=widgets.Layout(align_self='center'))

        controls_box = widgets.VBox([imgbox, exit_button], layout=widgets.Layout(align_self='center'))
        # ['auto', 'flex-start', 'flex-end', 'center', 'baseline', 'stretch', 'inherit', 'initial', 'unset']
    
-   Create the controls for the exit widget.

    .. code-block:: python

        def exit_button_Callback(value):
            global model
            model = 'Exit'
        #     with output: print(model)
        exit_button.on_click(exit_button_Callback)
    
-   Main process:

    The main function built for our main process is camera function. Within the function:

    1. Initialize the camera input, and the framerate. 

        .. code-block:: python

            # Open camera
            capture = cv.VideoCapture(1)
            
    2. Capture every frame from the camera on loop. Terminate the loop upon closure of the camera.

        .. code-block:: python
            
            while capture.isOpened():
               
        1. Import in the frame of the input feed and resize it to 640, 480 ratio. 

            .. code-block:: python

                _, img = capture.read()

                img = cv.resize(img, (640, 480))

        2. Process the input frame with our follow_face model.

            .. code-block:: python

                img = follow.follow_function(img)
            
        
        3. If the model is set to exit, close all the windows opened and release the camera.

            .. code-block:: python 

                if model == 'Exit':
                    cv.destroyAllWindows()
                    capture.release()
                    break
    
    3. To activate the function above, first activate a display output, then within a thread run the function.

        .. code-block:: python

            display(controls_box,output)
            threading.Thread(target=camera, ).start()