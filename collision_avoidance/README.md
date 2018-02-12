# Collision Avoidance

## Overview
The assignment is pretty straightforward. We give you information about a set of drones (their starting location and the waypoints they should travel to), and you make sure that the drones get to all their waypoints. The tricky part is, of course, making sure that drones don't crash into each other. 

## What's provided
I've written some basic code for: 
* Reading a json configuration file (specifying information about all of the drones)
* Connecting to Dronology
* Starting SITL and Dronekit Vehicles for each of the drones in the configuration file
* Completing the initial handshake protocols
* Starting a thread to send the state of each drone back to Dronology every 1 second. 
* Shutting everything down (on ctrl + c)

Source code is located in [main.py](https://github.com/smbayley/DronologyAssignments/blob/master/collision_avoidance/main.py) and [util.py](https://github.com/smbayley/DronologyAssignments/blob/master/collision_avoidance/util.py). 

An example test/configuration file is provided in [test.json](https://github.com/smbayley/DronologyAssignments/blob/master/collision_avoidance/test.json). This configuration has 3 drones, each with 5 waypoints that they must reach. 

As specified in the assignment, we must be able to run your program with:
```bash
python main.py <path_to_configuration_file>
```
I've added an [additional optional argument](https://github.com/smbayley/DronologyAssignments/blob/master/collision_avoidance/main.py#L140) (ardupath) in main.py. __To be safe, don't change any of the arguments that have already been specified, or the method signature of main.__ If you'd like to add additional __optional__ command line arguments and/or __keyword arguments__ to main, that is OK. You don't want to be the one that I'm unable to run your code because you changed the order of the arguments or removed an argument. :) 

## What's left?
You'll need to write code that makes sure drones get to all their waypoints without crashing into each other. Some things to consider:
* I recommend by starting with a distance function. You will need this later on for two reasons: to figure out how close a drone is to any other drone, and to figure out when a drone has reached its waypoint.
* Once you can compute distance, write some code that sends drones to their waypoints (sequentially) _without worrying about potential collisions_. Note: you should keep in mind that at some point, when you do handle potential collisions, you will need a way of performing an "avoidance manuever" and subsequently finishing the route to the current waypoint. Design accordingly!
* After making it this far (and verifying that things appear to be correct in the Dronology UI), you can start working on your collision avoidance algorithm. 
* Start with simple test cases and work your way up. 

## Rules
1. Drones must maintain an altitude between 20 and 40 meters at all times. 
2. Drones must reach every waypoint in their route. Getting within 3m of a waypoint is considered "reaching" it. 
3. Drones should stay within 500m of their starting location. 
4. Drones should travel at 10 m/s at all times except during collision avoidance maneuvers. 

## Final Notes
* Our evaluation will not use more than 10 drones. _You don't need to write an algo to handle hundreds of drones_. 
* We have not officially decided what constitutes a collision. I'm thinking that if the distance between any two drones is <= 1 meter, we will call that a collision. We will clarify this before the due date. 
* We will use _laser distance_ in our evaluation. For small distances (i.e., <= 5km) this is more accurate.  This means that if you use an approximation (e.g., [haversine](https://en.wikipedia.org/wiki/Haversine_formula)), your distance might not match our distance. If you want to be extra safe, just use a larger separation distance. In other words, if we say 1m equals collision, assume that you need to make sure drones don't get within 5m of each other. Alternatively, you can learn about [better ways to deal with geographical positions](http://nvector.readthedocs.io/en/latest/src/overview.html) (probably not the best use of your time).
* You can assume that all of our tests will be done in South Bend. You don't need to worry about discontinuities at the equator or singularities at the poles. 
* __Get started early!__ This is a difficult assignment. Try to be creative. We don't expect you to develop a perfect solution. However, it should be clear to us that you suffered while you were tyring to! ;) 

## Questions?
Email sbayley@nd.edu. If you have a question about the code or the instructions, I'm sure others are confused as well. Let me know!
