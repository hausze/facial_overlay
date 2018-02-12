This is the README text file for the list of tester source code which implemented for Kinect K2 Intrinsics and Extrinsics caliberation.
Created by H. Sze 04/27/2015

The two projects started with the goal of accurately calibrating the RGB camera to the Depth Camera, via versa, and across multiple systems pairs.
Initially, I implemented the OpenCV findChessboardCorners and findCirclesGrid algorithms.  While the result is satisfied for the RGB camera, it is not suitable for the depth camera due to the high noise-to-signal ratio.  Then, I divided up the components within the findCirclesGrid, and added
image processing and case-by-case parameter twisting.  In additional, I reduced the search area in the depth camera image by cropping, proportional to the result from the RGB image and the general scaling.  Lastly, I also implemented background subtraction for more robustness in circle centers 
detection.  There were two circle board designs:  4 circles design and 19 + 1 big circles design.  The fully executable source for the 4 circles design is the tester22.cpp.  The tester23.cpp is designed for the 19 + 1 big circles design.  
The developed tools from color to depth camera calibration were carried over to the system to system calibration.  The major hurtle was to setting up the point cloud library to accept streaming from multiple systems.  Furthermore, the image pixels to point cloud projection was a part of the
study as well. The testerpcl5.cpp is the source for multiple systems (only 2 for now but easily expandable) to detect an user-defined number of tie points, then project the result onto the viewer.  The testerpcl6.cpp is primarily for analysis of the mapping from the pixel coordinate to the point
cloud coordinate for one system.

To test/run any of the testerXX.cpp or testerpclX.cpp, simply change the LINE 47 on CMakeLists.txt in the aemass-scene-builder directory to the desired
cpp file.  Then go to the "build" directory on the Terminal and run " ./scene-builder -live 192.168.4.37 1321 192.168.4.30 1321 " for two systems live
or just " ./scene-builder -live 192.168.4.37 1321 " for a single system live on the desired ip address and port.

For Color to Depth Camera Calibration :
tester2.cpp : Initial test to use onboard webcamera for corner/circle detection and calibration parameters computation
tester3.cpp : Test Version to detect chessboard in both depth and color with Kinect, and calibration parameters computation
tester4.cpp : Lite Version test to detect Corners in color only to twist the algorithm setting
tester5.cpp : Lite Version test to detect Corners in depth only to twist the algorithm setting
tester6.cpp : Lite Version test to detect circles/feature in depth only
tester7.cpp : Lite Version test to detect circle in color only
tester8.cpp : Algorithm version of detected circle in color to crop depth
tester9.cpp : Algorithm version of detected circle in color to crop depth with rotated Rect
tester10.cpp : Algorithm version of detected circle in color to crop depth with algorithm to match the circles board from the circles detected in the depth
tester10redo.cpp : Stable Version test to detect circle in color, crop depth and detect circle in cropped depth
tester11.cpp : Version to detect circle in color then best guess the entire circles board
tester12.cpp : Version that work further on tester11 by implementing the same algorithms to the depth image and find its corresponding 121 circlesboard points
tester13.cpp : Improve tester11 by detecting overlaying circle on the chessboard circle matrix because of missed projection
tester14.cpp : Version that work further on tester12 by improving the algorithms to the color image only
tester15.cpp : Slightly modified from test12 to get center point as the tie_points for Wu
tester16.cpp : Detect circle in ver2 board with 4 circles and map to the Board
tester17.cpp : Extend tester16 to add on depth image as well
tester18.cpp : Implement background subtraction on the color image to improve circle detection
tester19.cpp : Expand tester18 to include depth image cropping and circle detection
tester20.cpp : Implement background subtraction on the depth image to improve circle detection
tester21.cpp : Add-on BackgroundSubtraction stable version for tester10redo.cpp to replace croppingS
tester22.cpp : Extend tester17 and enhance detection by background substraction
tester23.cpp : Modified tester22 for the pattern-circle-and-a-big-circle rig with new algorithms
tester24.cpp : The original version of tester23.cpp without any modular methods call (for best result, rotate the board 45 degree perpendicular to the camera)
tester25.cpp : Furthermore improve tester23.cpp and solve double free issue
tester26.cpp : Add on depth image pair by extending tester25.cpp
tester28.cpp : Extend tester26.cpp by improving the assigning boardcircle algorithm

For System to System Calibration :
testerpcl.cpp : tester to include pcl
testerpcl2.cpp : Initial test to include pcl for multiple systems
testerpcl3.cpp : barebone testerpcl.cpp with loaded headers
testerpcl4.cpp : extend testerpcl3 with extrinsic calibration (manually switching and point inputting calibration)
testerpcl5.cpp : extend testerpcl3 with extrinsic calibration  (automatically picking and switch)
testerpcl6.cpp : extend testerpcl5 to find out the transformation from pixel to point cloud coordinate
testerpcl7.cpp : for manually input transformation matrix for the point cloud
testerpcl8.cpp : extend testerpcl5 with the selected tie points plotting as a red dot
testerpcl9.cpp : extend testerpcl8 with averaging the depth value of the neighbors of the selected tie points to improve robustness problem due to the noise

