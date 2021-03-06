# Linux-projects
Project 1
________________________________________


In order to create simple calculator in linux script, we will use nano editor (type nano in terminal) to write our code. The following synthax which acts like swicth case in language c
will help us simplify the task :
----------------------------
case word in
   pattern1)
      Statement(s) to be executed if pattern1 matches
      ;;
   pattern2)
      Statement(s) to be executed if pattern2 matches
      ;;
   pattern3)
      Statement(s) to be executed if pattern3 matches
      ;;
   *)
     Default condition to be executed
     ;;
esac

--------------------------
The command read , read from user input the number, and the command echo acts like "printf". Now if we want to save we use ctrl+o
and then enter. If we have an error we can edit our file using nano <filename> but we should be in the same directory. Once we are done
we save and we type in terminal sh <filename> to execute our file. Since bc doesn't interpret float numbers we use scale=2 to calculate
float numbers with 2 digits after floating point. 

Project 2
________________________________________

   
   
First we type the command nano, to open a nano editor and we write our html code . Then we save it using ctrl+o and give it the name cv.html then enter and ctrl+x to quit. 
Now using the command browse (filename) without parentheses, and being in the same directory, we can easily expose the cv.html file via web browser. 



Project 3
________________________________________

First we install node js using the command sudo apt-get install nodejs-legacy. Once installation is complete, we install npm using sudo apt-get install npm. We can now proceed to node red installation, using sudo npm install -g --unsafe-perm node-red node-red-admin.Finally we type the command node-red and we type in the browser http://localhost:1880. Now the following video shows step by step how to do it : https://www.youtube.com/watch?v=tTqgzg4zmwk. To see the values on a dashboard, in a new browser we type "Raspberry ip:1880/UI. Once we are done, we export the project in "all flows default".


   
Project 4
________________________________________


In this project, we aim to establish communication between two raspberry pis, using the Mqtt protocol. 

1_The first task consists of publishing the sensors values of RP1(publisher), to RP2(subscriber) and display them on the
live dashboard of RP2. To start, on RP1, we create a python project and we call it ClientPublish(file uploaded on github)
and we execute it. Now we run node-red command on RP2 and use "mqtt in" modules. We should change each ones topic depending on the topic
that we subscribe to, for each sensor. If we want to make sure that everything is okay, on the RP2 node red window,
we should be able to see the same values when we connect to each mqtt module a msg.payload module in debug window.
Now we connect a gauge to each mqtt, and in the gauge settings we do small changes to be able to see the values correctly.
Nevertheless, we should choose in each MQtt module the localhost option, and the topic depending on the one that we published
to first, in the python file. The last thing to do is a small transformations to the values, in the python file. 


2_The second task is to publish a text message from RP2 to RP1(in this case RP1 is the subscriber) and to display it on 
its 8x8 led display.To do so, we start by connecting inject to mqtt out to be able to subscribe to the "textbox"topic, 
and msg.payload to be able to display the text saved in this module, on RP1 8x8 led display. Once we receive the message we'll be able to print it in the debug window on python(RP1) and we can now use the sense.show_message to display it. In our case we put hello world in the inject module.


!!!Pour aller plus loin!!!
In this last part, we use the same concept as part 2, but this time we do some coding to make some transformations on msg.payload in order to display the image published from RP2 on the RP1 display. Let's take the exemple of the question mark, defined as "image" in the clientsubscribe.py file. First we need to publish it so we paste the entire list with the commas, the spaces between characters and the brackets removed. Now we use data.decode("utf-8")  to transform it to a string and finally we convert it to a list using the function Convert(). Now that we can use the function sense.set_pixels to display it. 

Sources:
Part 1&2: https://www.rs-online.com/designspark/plug-and-play-iot-with-the-pi-sense-hat
Part 3: https://pythonhosted.org/sense-hat/api/

Please note the string-list transformations, such as the convert function and the transformations done to the accelero values were done by me.

Projet 5
______________________
   

For the series of project 5 tasks, we should first develop an application with node-red capable of reading BLE data and displaying them through a node-red dasboard. To start, we download the node-red-contrib-epi-bluetooth module using the command "npm node-red-contri-epi-bluetooth " to get BLE notify and input nodes. Now we drag a BLE-notify node to create a device that will be visivle to the connecting clients. So we start by adding a new device definition by clicking on the pen next to device and we add the name "My bluetooth Device". Now we add a service name and add a universallly unique identifier that we chose from the website https://www.uuidgenerator.net/ . Last but not least, we enter a GATT characteristic UUID for a particular node and click done. We still need to drag a ble in node and select the defined Device and Service that we just configured but we only add unique Characteristic UUID . now by adding the connection shown in ble flow.jpg , we will be able to subscribe from ble-notify, because it will push a notification event to active listeners. ble-in will receive inputs from connected clients. It is Write-Only and accepts JSON strings as ble notify, and that's why timestamp(inject node) should be configured as json to be accepted. Numbre 7 will be shown on dashboard.

The second part of project 5 consists of building a tiny raspberry Pi3 image with buildroot. To do so, we start by downloafing buildroot using the command : " git clone git://git.buildroot.net/buildroot  ". Once we are done we cd to build root directory and type the command "make raspberrypi3_defconfig". if we want to get ssh and wifi working for example, we type the command "make menuconfig" which will open up a promt that allows us to configure, but in my case i'll not enter in details. Finally by typing the command" make -j8 " we will download the image in buildroot/output/images directory and this operation takes roughly 30 minutes . Now we can go to raspberry pi imager ,choose os then use custom, and use the image sdcard.img (159.4 mbs as shown in sdcard size.jpg) then choose the sd card and write. The boot up operation takes few secondes.

Resources:
https://flows.nodered.org/node/node-red-contrib-epi-bluetooth
https://www.youtube.com/watch?v=yxj8ynXXgbk
