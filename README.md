# Stereoscopic 3D system for Unreal Engine 5

Today is my birthday and after 3 month of work with UE5 this release of the completed S3D system is like a present for me and you. :wink::+1:

![Stereo3D_Car](https://github.com/Vital-Volkov/Stereoscopic-3D-system-for-Unreal-Engine-5/blob/main/Unreal%20Engine%205%20Screenshot%202023.05.06%20-%2017.31.57.01_FPS.png)
![Stereo3D_Car](https://github.com/Vital-Volkov/Stereoscopic-3D-system-for-Unreal-Engine-5/blob/main/Unreal%20Engine%205%20Screenshot%202023.05.06%20-%2017.34.52.34.png)
![Stereo3D_Car](https://github.com/Vital-Volkov/Stereoscopic-3D-system-for-Unreal-Engine-5/blob/main/Unreal%20Engine%205%20Screenshot%202023.05.06%20-%2020.35.51.12_Car.png)
![Stereo3D_Girl](https://github.com/Vital-Volkov/Stereoscopic-3D-system-for-Unreal-Engine-5/blob/main/Unreal%20Engine%205%20Screenshot%202023.05.06%20-%2020.51.53.02_Girl.png)
![Stereo3D_Clouds](https://github.com/Vital-Volkov/Stereoscopic-3D-system-for-Unreal-Engine-5/blob/main/Unreal%20Engine%205%20Screenshot%202023.05.05%20-%2016.25.16.67_VolumetricClouds100mStereobase.png)

How it works:  

Just drop the main blueprint Actor rig with 2 Scene Capture cameras into a scene and it should make all other work automatically.  
It will search View Target in scene and active camera component and attach to it, copy post process settings from it(option) or use their own preset,
disable render of active parent Scene Camera(via ortho projection hack) for best performance(I got same performance as 2D in S3D Optimized mode 85fps in example FPS scene FullHD i512600K RTX2060)  
Render into S3D material shader which makes the required S3D output method from Left and Right view and draw the result to screen as Post Process material in parent Scene Camera.
Then you can make required S3D settings(100% realistic or Toy effect world) via Panel with popup tips(while hovering cursor on variable names over 1 second) or via keyboard hot keys(easily changeable in project)
and save as many different profiles as you like and last saved will autoload on next start.
I made autofocus on the control Panel so you can drag the slider or hover cursor on the input fields and scroll the mouse wheel or type numbers from the keyboard
and just move the cursor away and new values will apply without pressing Enter.

Here the main runtime settings on the Panel and their keyboard shortcuts:

`Enable S3D` - `Num *`  
On/Off S3D toggle.

`Swap Left-Right View` - `Shift + Num *`  
If you resize the window in an interlace method or have different left/right filters or color glasses you can always fast swap Left-Right images.

`Optimize` - `Alt + Num *`  
Render only half X or Y resolutions for S3D output methods like Interlace SideBySide OverUnder(TopBottom) where half resolution anyway lost so rendering at full resolution
give advantage only in clearer image in specific output method like interlace where interrow antialiasing cause more blurry image in native resolution but 
This is a must have future for SideBySide and OverUnder methods where you see the same clear image but have performance boost in my case 65 vs 85fps 31%.
I have an interlaced S3D monitor LGD2342P but I found the best method is to output as OverUnder via HDMI and set this mode in monitor settings so I have same clear picture
like in native interlace mode but at 31% faster with performance same as 2D which is incredible!

`VSync`  
While this is must have option even for 2D to avoid image ugly tearing to horizontal lanes and limit GPU redundant overload(lock frames to monitor Hertz)
this is required for my best OverUnder method as when image moving left/right then lower part of screen delay from upper part and if image for right eye is lower,
then when you turn or move to right you will see S3D depth become shallower and vise versa so VSync is especially required for OverUnder S3D method but I don't make it enable
automatically when OverUnder selected and you can see this effect by your own then enable VSync to see differences and just Save it with other profile settings.

`Screen Density` & `User IPD` - `Shift + Num +/-`  
For precision S3D like in real life you should be able to set your eyes IPD(Interpupillary Distance) on screen as images offset(66mm common for example), but how do you know it without a ruler on the screen?
The Best instrument for this is Screen Density! Once you set correct PPI(Pixels Per Inch) of your screen then you make all settings precision in real millimeters on the screen
no matter full screen or any window size you get your UserIPD in real mm and infinity S3D depth like in real life(eye axis near parallel when you looking at far objects like stars).
And the main thing is not to overshoot your UserIPD as you get abnormal eye angles(overshoot parallel and outside each other) and this is an abnormal situation and usually does not happen in real life
without optic distortions per eye and can cause discomfort.

`Virtual IPD` - `Ctrl + Num +/-`  
This is your virtual IPD in 3D game world and can be any size as you like without discomfort from 0(it will look like a 2D gigantic screen or image in space always at max S3D depth)
to any large numbers as you need(you can set Max limit in project preset). So you can untick from realistic VirtualIPD be same as UserIPD and set VirtualIPD for example lower
than your real IPD to simulate small creatures(small stereo base) world perception or set it to 10,000mm(100 meters stereo base) as I made while testing and look at
S3D volumetric clouds many kilometers in size like a toy with a very nice S3D feel. So think about this parameter like S3D perception world size scalar.

`MatchToUserIPD`  
Left it ticked if you want a realistic S3D view by default so Virtual_IPD will match to UserIPD and you only need to set ScreenDensity and your actual UserIPD in millimeters
to get a realistic S3D view.

`Field Of View`(FOV) - `Num +/-`  
Horizontal FOV in degrees for camera zoom control or just read this from cameras and keep external FOV control(option).

`Panel Depth` - `Alt + Num +/-`  
As I made the 3D widget panel in camera full frustum space for both eyes(and as result fully compatible with any S3D output method) so I added Panel Depth also as a separate setting.
You can set it from 1(always like common 2D UI panels exactly at screen depth) to infinity depth(Min/Max limit can be set in project preset). You can set Min to 0.5 if you like
and you get a panel depth feel between you and the screen at half distance to the screen. Any setting different from 1 gives you a wider view of the panel and I add additional edges offset
so you will not lose edges and get full camera frustum view space for both eyes for panel drag and drop, move to any corner as you like and also save its position with other settings.
Very large work was done for the S3D panel and I like how it works with any resolution or window size and also with black borders(Aspect Constrain UE5 camera settings with unlocked Window Preserve Aspect in UE5 Project Settings).
With some combination of settings the Panel may become closer than Near Clip Plane and disappear so just turn values back and it appears again(if you lose slider you can return value by keyboard or load saved preset by holding Num *).
If you need the panel to be visible with such close distance then set Near Clip Plane in UE5 Project Settings to lower than 1cm(0.01 for example because values lower than 1 are not applied via console command).

`Screen Distance`  
Calculated distance from view point to calculated by PPI real size of the viewport depending of Field Of View so If you seat at this distance from screen your Real FOV will match to virtual FOV
and you get 100% virtual/real view match wich is important for Flight Simulator view through screen like through cockpit window.

`Slot Name` - `Ctrl + Num *` for Save to any typed Slot Name and hold `Num *` for Load from Slot with typed Name.  
By default when no saved profile files exist or are removed then default Slot Name is User1 and when you Save to any name then 2 save files will be created
where one holding last save Slot Name from which autoload on next start and another the save Slot Name file itself with variables data.

All keyboard shortcuts control keys can be changed in the project as it uses Enhanced Input of UE5.

Here are UE5 project preset variables which can be changed before start and they are all in the S3D Setup group(variables outside this group are calculated at runtime and don't need to change them):

`S3D_EyePriority`  
An Important setting when you have a shooter with a camera set for Aiming by Right(or Left) eye so you just select the required scene camera eye and go.

`Widget_Open`  
The Widget with the S3D control panel is open or not at game start.

`Widget_MappingContext_Ignore`  
To stop shooting while you click on the panel like in the default FPS demo just select which Mapping Context to temporarily remove while the panel is open.
Looks like this is the simplest method to stop unwanted input as standard blueprint functions seem to have ignoring options for look and move input only.

`WidgetAutoShow_Time`  
For see settings changes made by keyboard shortcuts Panel will open(without cursor) 3 seconds after key release but will not block game input controls.
Set this to 0 and the panel will not auto open.

`WidgetSize_Keep`  
Keep size of the widget while resizing the viewport window or scale widget with window size.

`S3DMethodMat`
Select S3D default output method.

All variables like:  
`ScreenDensity`
`UserIPD`
`VirtualIPD`
and their `Min` `Max` values correspondingly must be Positive and most required will be checked at game start to turn from not correct negative input to correct using ABS(Absolute) function.

All variables with `_SetStep`  
Change step value for 1 tick frame while keyboard shortcut is pressed.
Can be set to negative for easy reverse keyboard +/- controls.

`Virtual_IPD_Max`  
Set maximum limit for keyboard and panel control of Virtual_IPD.
Use a low limit if you need precision controls near realistic values(like under 999 millimeters by default) or set it to huge numbers like 10,000mm(100meters)
to be able to see the world as a toy at runtime with maximum Virtual_IPD(huge stereoscopic base).

`FOV_Control`  
Any new camera FOV will be set to your S3D settings FOV and you control it by default but if you want default cameras FOV or need external FOV control then
untick it and it will only read FOV from cameras.

`FOV`  
This default FOV will be set if `FOV_Control` is enabled and filed to load at game start from a saved profile file with S3D settings.

`FOV_MinMax`  
FOV shouldn't be zero or 180 at planar projection not possible so the adequate limit is from 1 to 179 degrees for example but by default I set more realistic 10 to 170.

`WidgetDepth_ScreenDistanceMult`  
S3D Control Panel depth by default is the distance from viewpoint to your screen multiplicator so 1 means that the S3D panel will always look like a common 2D panel
because it is at screen depth.

`WidgetDepth_ScreenDistanceMult_MinMax`  
MinMax values for WidgetDepth_ScreenDistanceMult so if you want the S3D panel to be closer to you than a screen then 
you can set Min value below 1 but it should never be zero or negative.
Max value can be Infinity but you lose precision control at low values so 99 by default I think is far enough to see the difference with 999.
For example you sit before a 23 inch monitor and have realistic about 35deg FOV settings and ScreenDistance shows about 800mm * WidgetDepth 99 = 79200mm
So you feel like the panel at 79 meters looks almost like at infinity or like jet fighter HUD.

`PostProcessFromSceneCamera`  
Copy Post Process settings from Parent Scene Camera or use custom Post Process settings for S3D which can be preset in S3DCameraSettings struct variables.

`KillSceneCameraWhileS3D`  
Disable rendering of Parent Scene Camera via Ortho projection Hack(render Frustum set to zero via Width and Near/Far clip) while S3D is On
which boost performance from 43 to 67fps 56%! But default hit test will not work as it works only inside Camera frustum and stops working even due cut by near clip
which is nonsense for sure and ray hit testing should work independent from camera frustum and rendering. I haven't found easy method to avoid this now and you can just
tick off this Hack for fast solution to get working Top Down game demo scene where character moving by mouse click to position on floor but by performance cost as UE5 not have render layers like Unity to turn off
rendering of unnecessary objects. Or you can make a custom hit testing system like I do for S3D widget Panel and send ray to scene in perspective projection using mouse screen cursor position and Camera FOV.

`Debug`  
Print or not screen and log messages for S3D main blueprint.

There are also 2 preset variables in the Widget blueprint S3D Setup group:

`ToolTipDelay`  
Delay in seconds before the popup tip will appear when mouse hovering on the variable name of the Panel.

`Debug`  
Print or not screen and log messages for S3D Widget blueprint and edge corners.

Enjoy and welcome to donate to my crypto wallet:  
Bitcoin `bc1qf0af260q970f3ryrmlcde62jk4h6zhj08rkkjz`  
Litecoin `LVHktaDKWkyK96H2vcmvNWYx2nMkcysA2J`  
Or ask me and I will give you the required donate option.

Best regards,  
Vitaly Volkov  
vital.volkov@gmail.com
