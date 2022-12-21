import RPi.GPIO as GPIO
import time, datetime
import cv2
import yagmail

dateString = '%Y-%m-%d %H-%M-%S'
pir=8
buz=10

GPIO.setmode(GPIO.BOARD)
GPIO.setup(pir,GPIO.IN)
GPIO.setup(buz,GPIO.OUT)

GPIO.output(buz,GPIO.LOW)
time.sleep(5)
print("SENSOR is READY")

cam = cv2.VideoCapture(0)
n=1



while True:
    x=GPIO.input(pir)
    print(x)
    if x==1:
        GPIO.output(buz, GPIO.HIGH)
        print("ALERT!!!INTRUSION DETECTED at PIR1")
        n=1
        z= datetime.datetime.now().strftime(dateString)#STORING DATE AND TIME IN A VARIABLE
        print (z) #PRINTING THE DATE AND TIME OF INTRUSION
        
        while True:
            n = n+1
            ret, image = cam.read()
            cv2.imshow('Imagetest',image)
            k = cv2.waitKey(1)
            print(k)
            if n == 5:
                break
        path='/home/ampi/pranshul/'+str(z)+'.jpg' #DATABASE SECTION
        cv2.imwrite(path, image)
        cv2.destroyAllWindows()
        time.sleep(0.5)
        GPIO.output(buz,GPIO.LOW)        
        password = "jzalcxpfcwhswkvo"
        yag = yagmail.SMTP('pranshul366@gmail.com', password)
        content = [f"inruder detected at {z}",yagmail.inline(f"{path}")]
        yag.send(to='pranshul4782.be21@chitkara.edu.in' , subject = "intruder detected", contents = content)
