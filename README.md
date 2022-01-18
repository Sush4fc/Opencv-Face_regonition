# Opencv-Face_regonition
#count the number of faces on the video screen



import cv2 #pip installl opencv 
import numpy
import dlib # pip instal dlib

cap = cv2.VideoCapture(0)

detector = dlib.get_frontal_face_detector()

while True:
	ret, frame = cap.read()
	frame = cv2.flip(frame,1)

	gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
	faces = detector(gray)


	i = 0	
	for face in faces:
		x, y = face.left(), face.top()
		x1, y1 = face.right(), face.bottom()
		cv2.rectangle(frame, (x,y), (x1,y1), (0,255,0), 2)

		i = i+1

		cv2.putText(frame, "Face No" + str(i), (x-10, y-10), cv2.FONT_HERSHEY_SIMPLEX, 0.7, (0,0,255), 2)
		print(face, i)

	cv2.imshow("Count Number of Face, Press Q for Exit", frame)


	if cv2.waitKey(1) & 0xFF == ord("q"):# press q to exit
		break
print("Press Q for Exit")
cap.release()
cv2.destroyAllWindows()		
