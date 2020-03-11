# REAL TIME FACE DETECTION THROUGH WEBCAM USING OPENCV
 >import numpy as np
 >import cv2
 
 Download the haar cascade files in your directory and mention the path of haar cascade file within single quotes.
 
 
>faceCascade = cv2.CascadeClassifier('C:\\Users\\Vandana\\mini2\\haarcascade_frontalface_default.xml')


It loads the classifier from the file. Haar cascades are classifiers for object detection. The haarcascade_frontalface_default.xml is designed in opencv to detect frontal face.

>cap = cv2.VideoCapture(0)


This will return video from first webcam on your computer.

>cap.set(3,640) # set Width

>cap.set(4,480) # set Height

>while True:

>    ret, img = cap.read()

It captues 

>    #img = cv2.flip(img, -1)

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
