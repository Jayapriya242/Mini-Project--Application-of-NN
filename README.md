# Mini-Project--Application-of-NN

## Project Title:
    Shape detection
## Project Description 
      To peform the objective of the shapes detection model by identifying and detecting shapes of part of image.
## Algorithm:
1.	Importing required libraries.
2.	Show the input image, till someone hits any key.
3.	Convert the image to grayscale and show the image.
4.	 Detect edges from the gray image, and show them.
5.	Detect contours from the image with edges.
6.	Let’s traverse in contours. 
7.	Calculate the number of lines in contours using cv2.approxPolyDP() and let’s detect shapes using cv2. 
8.	If no. of lines equals 3, then it’s a triangle.
9.	If the no. of lines equals 4 then it’s either a rectangle or a square.
10.	If the difference between height and width is less than 5 pixels, then there’s a very negligible difference in width and height, it’s a Square. Else it’s a rectangle.
11.	 If no. of lines equals 10, it’s a star.
12.	If no. of lines equals 8, it’s a circle. Put the text in the center of every detected contour. We calculated the center coordinates of every contour using moments
13.	Draw the contours and show the image.
14.Show the output image.

## Program:
```
import cv2
import numpy as np
img = cv2.imread('someshapes.jpg')
cv2.imshow('1. original image', img)
cv2.waitKey(0)
gray_img = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
cv2.imshow('2. gray image', gray_img)
cv2.waitKey(0)
edges = cv2.Canny(gray_img, 50, 200)
cv2.imshow('3. edges', edges)
cv2.waitKey(0)
contours, hierarchy = cv2.findContours(edges.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_NONE)
for cnt in contours:
 approx = cv2.approxPolyDP(cnt, 0.03*cv2.arcLength(cnt, True), True)
print(len(approx))
    if len(approx) == 3:
        shape = 'Triangle'
        M = cv2.moments(approx)
        cx = int(M['m10']/M['m00'])
        cy = int(M['m01']/M['m00'])
 elif len(approx) == 4:
        x, y, w, h = cv2.boundingRect(cnt)
        if abs(w-h) < 5:
            shape = 'Square'
            M = cv2.moments(approx)
            cx = int(M['m10'] / M['m00'])
            cy = int(M['m01'] / M['m00'])
        else:
            shape = 'Rectangle'
            M = cv2.moments(approx)
            cx = int(M['m10'] / M['m00'])
            cy = int(M['m01'] / M['m00'])

    elif len(approx) == 10:
        shape = 'Star'
        M = cv2.moments(approx)
        cx = int(M['m10'] / M['m00'])
        cy = int(M['m01'] / M['m00'])

    elif len(approx) == 8:
        shape = 'Circle'
        M = cv2.moments(approx)
        cx = int(M['m10'] / M['m00'])
        cy = int(M['m01'] / M['m00'])

    cv2.putText(img, shape, (cx-30, cy),cv2.FONT_HERSHEY_SIMPLEX, 0.7, (0, 255, 0), 1)

    cv2.drawContours(img, cnt, -1, (0, 255, 0), 2)
    
cv2.imshow('cnt', img)
cv2.destroyAllWindows()
```
## Output:
INPUT IMAGE:

![nn-02](https://user-images.githubusercontent.com/114279259/205431846-71d9dfed-38e8-4905-bbea-440e82e65b1a.jpg)
DETECTED IMAGE:

![NN-01](https://user-images.githubusercontent.com/114279259/205431851-44c6d823-1565-4e6f-a86a-25ff691e7e37.png)
FINAL OUTPUT:

![nn-03](https://user-images.githubusercontent.com/114279259/205431866-698bdbed-5179-4704-8c1d-67f8f21fc2d8.png)


## Result:
Thus, The shape detection is implemented successfully.
