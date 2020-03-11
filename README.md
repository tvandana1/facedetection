# REAL TIME FACE DETECTION THROUGH WEBCAM USING OPENCV
    import numpy as np
 
    import cv2
 
 Download the haar cascade files in your directory and mention the path of haar cascade file within single quotes.
 
    faceCascade = cv2.CascadeClassifier('C:\\Users\\Vandana\\mini2\\haarcascade_frontalface_default.xml')

It loads the classifier from the file. Haar cascades are classifiers for object detection. The haarcascade_frontalface_default.xml is designed in opencv to detect frontal face.

    cap = cv2.VideoCapture(0)

This will return video from first webcam on your computer. If you have a secondary camera you can change 0 to 1.

    cap.set(3,640) 

It sets Width of the camera.

    cap.set(4,480) 

It sets Height of the camera. 

    while True:

It intializes infinite loop(to be broken by break statement).

    ret, img = cap.read()

It captures frame by frame through webcam. ret is boolean regarding whether or not there was a return at all,at the frame is each frame that is returned. If there is no frame, you won't get an error, you will get none.

    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

Here we define new variable, gray, as the frame, converted to gray. It is important to note that OpenCV reads colours as BGR(Blue Green Red), where most computer applications read as RGB(Red Green Blue). For the purpose of image recognition, we need to convert this BGR channel to gray channel, so that it is easy to process and is computationally less intensive.

    faces = faceCascade.detectMultiScale(

       gray,

It is input grayscale image.

        scaleFactor=1.2,

It is parameter specifying how much the image size is reduced at each image scale. It is used to create scale pyramid.

        minNeighbors=5,    

Parameter specifying how many neighbors each candidate rectangle should have to retain it. This parameter will affect the quality of the detected faces: higher value results in less detections but with higher quality.

       minSize=(20, 20)

Minimum possible object size. Objects smaller than that are ignored.

   )


    for (x,y,w,h) in faces:
        cv2.rectangle(img,(x,y),(x+w,y+h),(255,0,0),2)
        roi_gray = gray[y:y+h, x:x+w]
        roi_color = img[y:y+h, x:x+w]
 
 
The function will detect faces on image. Next, we must "mark" the faces in the image, using , for example,  a blue rectangle. 

This is done with this protion of code. If faces are found, it returns the positions of detected faces as a rectangle with the left up corner(x,y) and having "w" as its width and "h" as its height => (x,y,w,h). 

Once we get these locations, we can create an ROI(Region Of Interest) for the face and present the result with imshow() function. cv2.rectangle function takes in the arguments frame, upper left coordinates of the face, lower right coordinates, the RGB code for the rectangle(that would contain the detected face) and thickness of rectangle. 

The roi_gray defines the region of interest of the face and roi_color does the same for original frame.
 

    cv2.imshow('video',img)
    
Displays the resulting frame .
Syntax: cv2.imshow(window_name,image) => window_name representing the name of the window in which image to be displayed and image to be displayed.

    k = cv2.waitKey(30) & 0xff
    
cv2.waitKey() is a keyboard function. Its argument is the time in milliseconds. The function waits for specified milliseconds for any keyboard event. If you press any key in that time, the program continues. If 0 is passed, it waits indefinitely for keystroke. It can also be set to detect specific key strokes.

cv2.waitKey() returns a 32 Bit integer value. The key input is in ASCII which is an 8-bit integer value. So you can only care about these 8 bits and want all other bits to be zero. This you can achieve with the above code. 0xff is the hexadecimal number FF which has integer value of 255.
    
    if k == 27: # press 'ESC' to quit
        break

Press ESC to quit.

    cap.release()

    cv2.destroyAllWindows()
