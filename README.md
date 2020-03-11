# REAL TIME FACE DETECTION THROUGH WEBCAM USING OPENCV
 >import numpy as np
 
 >import cv2
 
 Download the haar cascade files in your directory and mention the path of haar cascade file within single quotes.
 
 >faceCascade = cv2.CascadeClassifier('C:\\Users\\Vandana\\mini2\\haarcascade_frontalface_default.xml')

It loads the classifier from the file. Haar cascades are classifiers for object detection. The haarcascade_frontalface_default.xml is designed in opencv to detect frontal face.

>cap = cv2.VideoCapture(0)

This will return video from first webcam on your computer. If you have a secondary camera you can change 0 to 1.

>cap.set(3,640) 

It sets Width of the camera

>cap.set(4,480) 

It sets Height of the camera 

>while True:

It intializes infinite loop(to be broken by break statement)

>    ret, img = cap.read()

It captures frame by frame through webcam. ret is boolean regarding whether or not there was a return at all,at the frame is each frame that is returned. If there is no frame, you won't get an error, you will get none.


>    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

>   faces = faceCascade.detectMultiScale(

>       gray,

>        scaleFactor=1.2,

>        minNeighbors=5,    

>       minSize=(20, 20)

>   )


    for (x,y,w,h) in faces:
        cv2.rectangle(img,(x,y),(x+w,y+h),(255,0,0),2)
        roi_gray = gray[y:y+h, x:x+w]
        roi_color = img[y:y+h, x:x+w]
        

    cv2.imshow('video',img)

    k = cv2.waitKey(30) & 0xff
    if k == 27: # press 'ESC' to quit
        break

cap.release()
cv2.destroyAllWindows()
