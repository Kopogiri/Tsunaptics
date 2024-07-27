# Tsunaptics Headpat Haptics Hardware

A hardware offshoot of Senseshift to create headpat haptics. 

Senseshift GIT https://github.com/senseshift \
Senseshift Docs https://docs.senseshift.io/ 

This is a short list of parts and a guide to make headpat haptics using Senseshift and 
altering the usage of the facial interface haptics option.
Please read Senseshift Docs before this. 

PARTS - \
[ESP32 D1Mini](https://www.aliexpress.com/item/1005006661449926.html?) \
[TP4057 Charge Board](https://www.aliexpress.com/item/1005004987359215.html?spm=a2g0o.order_list.order_list_main.10.5bb01802lKHa9X) \
[ULN2803AG Transistor Array](https://www.aliexpress.com/item/1005004008730216.html?spm=a2g0o.order_list.order_list_main.75.5bb01802lKHa9X) \
[Micro DC Vibration Motor](https://www.aliexpress.com/item/1005004438162130.html?spm=a2g0o.order_list.order_list_main.95.5bb01802lKHa9X) \
[804040 LiPo Battery](https://www.aliexpress.com/item/1005005247964640.html?spm=a2g0o.order_list.order_list_main.65.5bb01802lKHa9X) \
[Switch](https://www.aliexpress.com/item/4001207529493.html?spm=a2g0o.order_list.order_list_main.150.5bb01802lKHa9X) \
A Kitchen Sponge (not a joke)

You can also go without the charge board / battery and power the device straight from 
the USB port of the D1Mini if you want to.

# Guide -
If you are using the carrier board please change the following code in the Senseshift 
firmware -
SENSESGHIFT-FIRMWARE > firmware > mode_configs > bhaptics > tactal.cpp
Make the code here match on line 32
```
void setupMode()
{
    // Configure PWM pins to their positions on the face
    auto faceOutputs = PlaneMapper_Margin::mapMatrixCoordinates<AbstractActuator>({
      // clang-format off
      
      {new PWMOutputWriter(05), new PWMOutputWriter(23), new PWMOutputWriter(19), new PWMOutputWriter(33), new PWMOutputWriter(18), new PWMOutputWriter(26)},
      // -------------Node 01-------------------Node 02------------------Node 03------------------Node 04------------------Node 05------------------Node 06---
      // clang-format on
    });
```
Then flash the firmware to the D1 Mini.

Solder the Switch, ULN and TP4057 to the carrier board.
Carrier board Gerber [here](https://github.com/Tonouda/a-bunch-of-junk/raw/main/HeadpatHapticsGerber.zip). You can order these from places such as JLCPCB or PCBWay.
![alt text](https://github.com/Tonouda/a-bunch-of-junk/blob/main/tsunaptics001.png?raw=true)

Solder standoffs to the relevant pins written on the board and then solder the D1 Mini to the board. \
![alt text](https://github.com/Tonouda/a-bunch-of-junk/blob/main/tsunaptics002.png?raw=true) \
Now connect the battery to the underside of the board. Red to Bat+ and Black to Bat-.

Alrighty! Now print the hapticsholdingthingy.stl. [here](https://github.com/Tonouda/a-bunch-of-junk/blob/main/HapticHoldingthingy%20v1.stl) or [here](https://github.com/Tonouda/a-bunch-of-junk/blob/main/HapticHoldingthingy%20v2.stl) It is currently made to fit an aftermarket 
Quest 2 strap through it. So feel free to edit it to fit your desired strap size or re create 
the jig entirely. \
![alt text](https://github.com/Tonouda/a-bunch-of-junk/blob/main/Screenshot%202024-04-01%20233346.png?raw=true) \
Once printed, you can drop the assembly into the middle bit. It should fit nice and snug.

Now grab your kitchen sponge and cut it into 6 pieces.
Cut 2 slits into each piece. 1 near the top (hard part of the sponge) and 1 in the middle.
You can then insert the arms of the jig into the top slits of the sponge and a motor into 
the middle slits. The sponge allows for the haptics to give a softer and more natural feel 
whilst also stopping the single motor from vibrating the whole entire thing because of its 
rigid body. Trust me, I have made this mistake, it sucks and this is sooo much better.
Lastly you can either solder XH JST connectors to the 4 pin holes or solder the motors 
directly to the board. 
The 3v3 pins are for the live (RED) wires. 
The M1 – M6 pins are for the ground (BLACK) wires.
In the firmware, M1 should correlate to Node 01 / Output 05 , M2 correlating to Node 2 / 
Output 23, etc.
Currently this is a bit jank due to bhaptics being weird and messing stuff up constantly 
with their updates. I’ll revise this at some point. This can easily be remedied in the 
avatar editing part of this guide so don’t worry too much right now.
Try it out on your head and see how it feels and fits.
You can heat up the arms in the middle with a heat gun to make the plastic malleable 
and slightly bend the arms to fit the roundness of your head.

You should now have something that looks like this (ish). Yours can be so much neater 
and tidier. This is a mess of experimenting, trial and error. \
![alt text](https://github.com/Tonouda/a-bunch-of-junk/blob/main/Screenshot%202024-04-01%20233635.png?raw=true) \
Test it with the bhaptics software and make sure all the motors work.

# OKAY NOW ITS TIME TO EDIT THE AVATAR!!! YIPPIE? -
Firstly watch [this youtube video](https://www.youtube.com/watch?v=QCtdo5_cYdk&ab_channel=PxINKY). It’s great! It will do most of the work for you. Get the 
facial interface imported. \
If the files provided don't work. Try and use [this](https://github.com/Tonouda/a-bunch-of-junk/raw/main/av3-animator-as-code-main%20(1).zip) file instead.

At this point make sure that the facial interface is attached to the HEAD in the armature 
list. See example- \
![alt text](https://github.com/Tonouda/a-bunch-of-junk/blob/main/Screenshot%202024-04-01%20233702.png?raw=true)

In the Inspector, you can untick the Mesh Renderer to hide the face plate. \
![alt text](https://github.com/Tonouda/a-bunch-of-junk/blob/main/Screenshot%202024-04-01%20233709.png?raw=true)

Awesome! 
Now click on the arrow to the right of Head in the armatures list to open up the prefab. \
![alt text](https://github.com/Tonouda/a-bunch-of-junk/blob/main/Screenshot%202024-04-01%20233713.png?raw=true)

It will look like this. \
![alt text](https://github.com/Tonouda/a-bunch-of-junk/blob/main/Screenshot%202024-04-01%20233718.png?raw=true)

You can go ahead and hide Head_Motors in the Inspector. You wont need to see those.
As a quick explanation, the Others drop down is contacts used to interact with Other 
people in Vrchat whist the Self drop down is contacts used just for your own avatar to 
interact with itself. It is good practice to keep the relevant nodes the same in both drop 
downs. eg, Node 1 need to have the same values in both Other and Self. \
Let’s explain a bit more so you can get exactly what you want out of haptics! This is 
Node 1 used as an example.
Transform - The position is where the node will sit on the avatar. The Rotation and Scale 
really don’t matter.
VRC Contact Receiver - The Shaps Type is exactly what you think, it is the shape of the 
contact. The ideal type is Sphere but you can change to suit your needs. The Radius is 
the actual size of the Sphere in this case. You can edit this again to suit your needs. 
Position and Rotation here don’t matter.
The filtering now should make sense. Self, Other, and Local. You can set these up with 
animators to create toggles if you are worried about getting overwhelemed. You can 
turn off the haptics from within VRC this way if you want.
Collision Tags is also important in the same sense. By defult they have Head, Hand, 
Finger and Foot. You can see that I have only kept hand and finger as I don’t wish to be 
headbutted or kicked in the head.
And that should be everything you need to know. \
![alt text](https://github.com/Tonouda/a-bunch-of-junk/blob/main/Screenshot%202024-04-01%20233725.png?raw=true)

The last job is to position the nodes to fit your avatar.
As I mentioned earlier, the firmware and bhaptics is wacky. 
The nodes for me work like so- \
![alt text](https://github.com/Tonouda/a-bunch-of-junk/blob/main/Screenshot%202024-04-01%20233733.png?raw=true)

Then you’re good to go!
Upload your avatar, jump into VR, grab a friend and get them to test it for you!
Have fun!!

Lots of love,
Kopo
