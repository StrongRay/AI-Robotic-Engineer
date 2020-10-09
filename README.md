# AI-Robotic-Engineer
Skills for the future - What skills does an AI Robotic Engineer requires ? Whoever tells you RPA (Robotic Process Automation) deserves to get shot =)

The purpose of the article is to give the readers a glimpse of what kind of skills are needed for the future in the area of robotics and AI.  The perspective of AI is discussed together with an example of robotics by NParks for a social distancing “dog” to a prototype that I developed to uncover the various skills needed for this kind of future.  Knowledge will only grow more complex.  But you will need certain foundation.  A moral principle then becomes, if it’s not AI, let’s not call everything AI. 

![What is AI](https://github.com/StrongRay/AI-Robotic-Engineer/blob/main/What-is-AI.jpg)

I love the [simple flow chart from MIT Technology Review](https://www.technologyreview.com/2018/11/10/139137/is-this-ai-we-drew-you-a-flowchart-to-work-it-out/) on how you define Artificial Intelligence.  The mumbo you get when every vendor jumps on the AI wagon and says they are doing Artificial Intelligence.  Anything complex should be made simple. And this flow chart is simple. Actually, computer visioning and image processing is technically not AI,  AI is more than computer visioning. 

#  The foundation of Self driving cars and CCTV human recognition

From cameras tracking humans to self driving cars, a large part must be the image processing capabilities to “recognize” images such as another car or obstacle, human, etc and upon detection do something with the data, it could be to steer the vehicle to avoid these obstacles or to send the data to another subsystem, trigger voice to warn people to wear masks, maybe even to drop a payload by a drone when an enemy commander is detected.   They all involve a few aspects – Hardware and Software Integration.   In the past, these disciplines are all quite specialized and involved lots of “software codes”.   With “libraries”, there is still some programming needed.  The realms of knowledge increases with each sub-specialty.  It’s like asking a brain surgeon to do an open heart surgery or a Japanese chef to cook Hainanese Chicken Rice. There could be basic foundations to learn, but the deeper the specialization, the harder it is to “copy” without being experimental. 

![SPOT-NPARKS-IMDA](https://github.com/StrongRay/AI-Robotic-Engineer/blob/main/Spot-NPARKS.jpg)

An example is the use of SPOT Robot by Boston Dynamics.  Nparks used this together with the help of IMDA to help program a cute distance enforcement alert dog.  In our Singapore journey of being a smart nation, One look and a layman can easily be led to think that it’s Artificial Intelligent and we are a smart nation.  There is a Chinese phrase “外行看热闹，行家看门道” translated to mean, those who are not in the know will be taken by the show-and-tell while the experts dig in and find out beyond the smoke and mirrors, how does the technology work.

Boston Dynamics has a great robot (https://www.bostondynamics.com/spot/technology) (USD 75K ?) https://www.youtube.com/watch?v=nkcKdfL7G3A) cute yellow “doggie” robot.  China version is not too far off (https://www.unitree.com/products/a1) but obviously a lot cheaper.  Look at the end section for the skills they are looking for.
Now, back to the NPark SPOT, on top of the robot is mounted with “open air equipment” If you stare closely, everything is kind of very exposed to the weather.   Not sure if this is can handle the rain fall.  There is a command center nearby controlling this unit and is likely relaying info either through WIFI or via a telco LINK.   Thus this is “Remote Control” (see picture below)  The use of this term is very important, it means Humans are manually sending instructions to the robot instead of the robot doing it’s own thing.  Hence, the AI is in the brains of the guy moving the joy stick.

Now, back to the NPark SPOT, on top of the robot is mounted with “open air equipment” If you stare closely, everything is kind of very exposed to the weather.   Not sure if this is can handle the rain fall.  There is a command center nearby controlling this unit and is likely relaying info either through WIFI or via a telco LINK.   Thus this is “Remote Control” (see picture below)  The use of this term is very important, it means Humans are manually sending instructions to the robot instead of the robot doing it’s own thing.  Hence, the AI is in the brains of the guy moving the joy stick.

![SPOT-NPARKS-IMDA-1](https://github.com/StrongRay/AI-Robotic-Engineer/blob/main/Spot-NPARKS-1.jpg)

The Intel RealSense Camera ( ready component) is used and so is the entire Boston Dynamics SPOT.  So the add-on is kind of pretty ugly with cable ties but it surfice as a POC.  So what is interesting is not whether you need to build all the components on your own, but to see how to integrate the stuff you get off the shelf and form a system.  
There is an out of the box controller of the BOSTON Dynamics SPOT which is an android based controller that can access the in-built Camera system.  Hence, begs the question, why have cameras on top when out of the box, the “dog” already has cameras. 

![SPOT-NPARKS-IMDA-2](https://github.com/StrongRay/AI-Robotic-Engineer/blob/main/Spot-NPARKS-2.jpg)

Given that its human control, one can deduce that the Boston Dynamics Software Development Platform is not used https://dev.bostondynamics.com/readme 
https://github.com/boston-dynamics/spot-sdk/tree/master/python/bosdyn-client has nice Python accessable codes to control the robot
https://www.smartcitiesworld.net/AcuCustom/Sitename/DAM/022/Spot_Bishan_park_1_GovTech_Singa_rm.jpg
The next part of this article is to share how this can be learnt on your own, through a variety of equipment and tools.  In particular, 

# Gist of Mini Proof-of-Concept (POC) 

The idea is to link up GPU-based hardware and write software to detect the center of the face and control the servos when the face center position 

# Hardware used 

The CPU is the 6 core GPU NVIDIA XAVIER NX.  To drive up the 2 servo motors, I used a 16 Channel 12-bit Pulse Wave Modulation PWM PCA9685 (from TaoBao it’s only S$3.50 w/o shipping) An additional 5V voltage can be supplied to the green pins except that I tap on the 5V from the XAVIER GPIO pins.  The servo motors are a pair of quite study industrial grade RDS3115 Digital Servo Motors and not those flimsy plastic looking SG90 servo motors.  The camera is a compatible Pi like Camera but this version I got can even give higher resolutions are higher frames per seconds. Good enough to do the job.

![XAVIER-1](https://github.com/StrongRay/AI-Robotic-Engineer/blob/main/ARTICLE-1.jpg)

# Software Engineering

Software Engineering has never change much.  You still need to do breakdown of work into simpler manageable parts and then debug at component level.  There are many times in reaching the final outcome, that it became challenging as troubleshooting hardware, sometimes, it’s a loose cable and/or GPIO config.  In one instance, I reconfigured my NVIDIA GPIO until it booted in #bash and I almost thought I lost my codes and NVIDIA system.  It was scary to loose control of the entire GPU hardware.  Luckily with stackoverflow, I managed to locate similar recovery and figured out how to modify the boot up parameters and managed to save my board.  It involved sed on extlinux.conf. It was very scary as you boot in bash with a prompt and there is nothing you can do to get back to the gui. 
Also, initial camera quality was quite bad and I adjusted to the right parameters and the camera is capable of getting the right details.  The software part is manageable but I opt for Python Multiprocessing and learnt to send signals to terminate all processes.  Also, revised my basics of cv2 to the next level and brushed up on python skill.  You cannot be manipulating images using OpenCV without delving into numpy.  

# The software


