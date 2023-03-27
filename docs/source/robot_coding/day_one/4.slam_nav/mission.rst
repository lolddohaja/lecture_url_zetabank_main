Mission
=========

.. raw:: html

    <div style="background: #ffe5b4" class="admonition note custom">
        <p style="background: #ffbf00" class="admonition-title">
            Project Name: Applying Navigation System on our Zetabot
        </p>
        <ul>
            <li><strong>-</strong> This mission is a <strong>group project</strong>.</li>
            <li><strong>-</strong> Construct a map within your team.</li>
            <li><strong>-</strong> Navigate the contructed map with the Zetabot as a team.</li>
            <div>
        </ul>
    </div>

Constructing a Map (as a Team)
--------------------------------

For our navigation mission, we we hold a cooperative mission with other teams.

- For each team, 3 map panels will be given.
- As a team try to arrange the panels so that there is a clear starting and finishing zone. For example:

  .. thumbnail:: /_images/autonomous_driving/day_one/arrangement.png


Mapping the Constructed Map
----------------------------------------------

Place the Zetabot on the starting location of the map. 


You can see the following screen by opening your web browser and accessing 10.42.0.1:5000:

.. thumbnail:: /_images/autonomous_driving/day_one/web_view_add.png

1. Select the Mapping button. 
   
   - This will start the mapping simulation. Using SLAM method, the robot will utilize its LIDAR sensors as well as multiple odometry sensors to map out its immediate surroundings. 
   - By using the controller, move the Zetabot around the constructed map to learn its surroundings.  
     
     .. thumbnail:: /_images/autonomous_driving/day_one/web_nav.png


Executing Navigation
---------------------

Place the Zetabot in the starting position. 

- Click on ``Start Nav Goal`` and click the desired location and drag the curser to set which direction the robot should face once it reaches the said location. 
  
  .. thumbnail:: /_images/autonomous_driving/day_one/web_start_nav.png

Team Competition
---------------------

- With other team members, construct a large map with starting and finishing position. Example:
  
  .. thumbnail:: /_images/autonomous_driving/day_one/team_final.png

- Team by team, execute the navigation task with your Zetabot. 