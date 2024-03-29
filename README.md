# Virtual_Painter
A simple openCV project to draw on a virtual canvas developed as I am trying to learn applications of openCV.

## No mediapipe
I tried using mediapipe and tracking my index finger for the painting but it is much more unstable and cannot handle fast movements which is why I went with with a method which instead uses color tracking to track an object(pen) of a specified color to draw instead of the user's hand.

## Method
* For tracking the "pen" a mask is created which looks for the closest/largest object of a chosen color (color of your pen). By default I have initialized it to blue but you can change it using the color trackbar.
* Erosion reduces the impurities present in the mask and dilation restores the eroded main mask.
* The mask is then added on top of the live video feed for the user to see their drawing in real-time.
* The drawn points are stored and the canvas created is stored as a png when the user quits the program.

## Algorithm
* Start reading the frames and convert the captured frames to HSV colour space.
* Prepare the canvas frame and put the respective ink buttons on it.
* Adjust the trackbar values for finding the mask of coloured marker.
* Preprocess the mask with morphological operations.(Erosion and dilation)
* Detect the contours, find the center coordinates of the largest contour and keep storing them in an array for successive frames.
* Finally draw the points, stored in the array, on the frame (live feed; so you can see the drawing in real-time) and, later, on the canvas.
* If the user quits, store the canvas as a png and destroy all open windows.

# Demo
![Demo](https://github.com/Rai-Sama/Virtual_Painter/blob/master/Demo.gif)

## Further points
* A "clear all" button is added which clears all the drawn points but there's no eraser. An eraser can be added by creating an eraser button, but to see it's effect properly, selecting it should change the drawing color to black and the canvas will have to be converted to a gray image and inverted and then superpositioned on the live feed, nullifying the previous drawings on the points that were colored by the eraser.
