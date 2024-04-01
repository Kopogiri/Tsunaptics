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
'''
void setupMode()
{
    // Configure PWM pins to their positions on the face
    auto faceOutputs = PlaneMapper_Margin::mapMatrixCoordinates<AbstractActuator>({
      // clang-format off
      
      {new PWMOutputWriter(05), new PWMOutputWriter(23), new PWMOutputWriter(19), new PWMOutputWriter(33), new PWMOutputWriter(18), new PWMOutputWriter(26)},
      // -------------Node 01-------------------Node 02------------------Node 03------------------Node 04------------------Node 05------------------Node 06---
      // clang-format on
    });
'''

