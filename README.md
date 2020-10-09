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

![XAVIER-2](https://github.com/StrongRay/AI-Robotic-Engineer/blob/main/ARTICLE-2.jpg)

The graphing system has some bells and whistles. Added a custom True Type Font TTF to highlight on the X and Y axis and move it as and when the new Face Box center is defined. Toggle guidelines can be done by G. R – resets the servos to (90,90) 

**cv2.CascadeClassifier** is being used with **Haarcascade_frontalface_default.xml**
**detectMultiScale** helps to identify the faces
Based on the face rectangle, the corresponding pan and tilt angles are obtained
A separate process makes use of these angles to move the servos  

Yeah, a true blue AI engineer will by now roll his/her eyes and say cv2.CascaseClassifier is not AI, no trained models =)  But the goal is that each code can be replaced like with MTCNN or a custom trained tensorflow model or YOLO v4 model.  Whatever it is, it’s another set of skills and exploration.

Why the code works on detecting faces, detection can be via hand, fingers, etc recognition.  Modular coding means that each detection method can be replaced by functionalities and the rest of the code , such as the graphing and servo movement, can still be used.

# Here’s how it looks

<a href="http://www.youtube.com/watch?feature=player_embedded&v=ycEKB1FtqS8" target="_blank">
  <img src="http://img.youtube.com/vi/ycEKB1FtqS8/0.jpg" alt="20 Hours" width="640" height="480" border="0" /></a>

# Lessons learnt

1.	Comment your codes as you need to remind yourself what has been done and why a value is placed. Always save your codes so that you can revert to your last working copy.
2.	After the boot up to #bash scare, backup your software codes so that if you need to get back your hard work
3.	Python is interpretive and no compilation is needed, it’s sufficient to use it for quick learning.   If codes are in C++, it should be more secure (protect your IP) however, the ideas are all copiable and reverse engineerable. There is no real IP.  It’s a combination of coding skills that you need.  The more you stuff you add, the rarer is the skill set
4.	Make your software modular, so you can verify each individual parts and then combine as a whole.  
5.	Multiprocessing python makes it interesting to spin off code segments dedicated to particular tasks.  The key is in passing information between processes. Global doesn’t quite work, you got to use namespaces.  
6.	The joy is in seeing the servo motors move in response to the location of the face.  And the pan and tilt moves in sync
7.	Can expand the detection into a generic class and then have child classes with each detection type

# If I am a student or someone looking to develop skills

The china group unitree, https://www.unitree.com/careers gives a glimpse on the jobs available in China and the skills they are looking for. 

![SKILLS](https://github.com/StrongRay/AI-Robotic-Engineer/blob/main/Skills.jpg)

By the way, 20,000 – 40,000 RMB divide roughly by 5, gives S$4,000 to S$8,000 per month for a robotic engineer, which by China standard quite a respectable monthly pay.  STM32 is a microcontroller, presumably used by the Robot.  I shall attempt to classify the skill type needed for a job role in a similar nature.
Any IT professional will need to be multi-skilled.  The skills must and will include soft and hard skills.  Soft skills refers to skills likely transportable and relatively constant across years. Hard skills are specific knowledge on a specific area of knowledge.  A true team contributor must be able to have both soft and hard skills.  So I am going to classify the skills into various grouping.  The list is not prescriptive and is an instance of time in 2020, and no single person has all these skills.  But while a maths teacher is not a science specialist, the maths teacher needs to know basic physics, chemistry  and biology.  

![S-1](https://github.com/StrongRay/AI-Robotic-Engineer/blob/main/Skills-1.jpg)
![S-2](https://github.com/StrongRay/AI-Robotic-Engineer/blob/main/Skills-2.jpg)
![S-3](https://github.com/StrongRay/AI-Robotic-Engineer/blob/main/Skills-3.jpg)

While the list is not perfect and will change across time, there is no way one can say they can be a one-man show and can do everything.  There is a need for generalist as well as specialist.  What one can do is to ask “Am I interested in this domain because of passion or because of the money”.  If it is the later, life will be tedious if one hates debugging.  But passion cannot feed the family nor provide for fine dinning to court your partner.  But I believe you cannot choose to specialize at say, RPG programming on the AS/400 when the jobs out there are rare.  You will need to stare into the crystal ball and read a lot on the web to see how to shield yourself from being obsoleted.  The all important skill becomes the ability to learn, unlearn and relearn.  Abit of a cliché but true.  The moment the course material is created, a newer version is released.  That is why self-directed learning becomes ever more important.  

# Acknowledgement and useful links 

Absolute one must to count the pins and make sure you plug in the right GND and VCC https://www.jetsonhacks.com/nvidia-jetson-xavier-nx-gpio-header-pinout/

Servo control using CircuitPython is a set of library to control the servos 
https://learn.adafruit.com/16-channel-pwm-servo-driver/python-circuitpython

Pan Tilt Tracking with Pi and OpenCV [base code which I morph into current code]
https://www.pyimagesearch.com/2019/04/01/pan-tilt-face-tracking-with-a-raspberry-pi-and-opencv/

