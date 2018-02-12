# Collision Avoidance

This is your one stop shop for collision avoidance resources. Hopefully the instructions and code provided here will be useful. Let me know if that's not the case! 

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

## What's left?
You'll need to write code that makes sure drones get to all their waypoints without crashing into each other. Some things to consider:
* I recommend by starting with a distance function. You will need this later on for two reasons: to figure out how close a drone is to any other drone, and to figure out when a drone has reached its waypoint.
* Once you can compute distance, write some code that sends drones to their waypoints (sequentially) _without worrying about potential collisions_. Note: you should keep in mind that at some point, when you do handle potential collisions, you will need a way of performing an "avoidance manuever" and subsequently finishing the route to the current waypoint. Design accordingly!
* After making it this far (and verifying that things appear to be correct in the Dronology UI), you can start working on your collision avoidance algorithm. 
* Start with simple test cases and work your way up. 

## Final Notes
* We have not officially decided what constitutes a collision. I'm thinking that if the distance between any two drones is <= 1 meter, we will call that a collision. We will clarify this before the due date. 
* We will use _laser distance_ in our evaluation. For small distances (i.e., <= 5km) this is more accurate.  This means that if you use an approximation (e.g., [haversine](https://en.wikipedia.org/wiki/Haversine_formula)), your distance might not match our distance. If you want to be extra safe, just use a larger separation distance. In other words, if we say 1m equals collision, assume that you need to make sure drones don't get within 5m of each other. Alternatively, you can learn about [better ways to deal with geographical positions](http://nvector.readthedocs.io/en/latest/src/overview.html) (probably not the best use of your time).
* You can assume that all of our tests will be done in South Bend. You don't need to worry about discontinuities at the equator or singularities at the poles. 
* __Get started early!__ This is a difficult assignment. Try to be creative and have some fun with it. We don't expect you to develop a perfect solution. However, it should be clear to us that you suffered while you were tyring to! ;) 

## Questions?
Email sbayley@nd.edu. If you have a question about the code or the instructions, I'm sure others are confused as well. Let me know!
