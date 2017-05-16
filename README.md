# D5M_CAMERA_ZYNQ

#### Color and Edge Detection Using FPGA Based Smart Camera ***(ALTERA CYCLONEII VERSION)***
#### ENTS 689Y Multimedia Communications over Networks
#### By
#### Sakinder Ali
#### Under the Supervision Of
#### Dr. Q. Zang


1. Abstract:
> Object recognition and tracking with real-time smart camera plays an important role in many modern vision applications such as work force tracking, intelligence surveillance, fire detection and many more. The main motivation of this project is to extract the color object and recognition using the Sobel edge detection and pass the detected signal to wireless channel using Zigbee (802.15.4). Experimental results demonstrated that object detection is very important for selected color tracking in the industrial automation and work places. Computer based Software programming such as java, C++ and C# cannot satisfy the speed in terms of real-time parallel processing of vast amount of video data. Therefore in order to improve the performance of real time video processing, FPGA is an effective device to rely on. This device is capable of real-time parallel processing of vast amounts of video data. The presented results from given design can be used as color and edge detection on a streaming video which is the basic building block necessary for further object detection.

> For detection of edge, various detection operators are used. Most of these operators are applied with convolution masks and are based on differential operations. 

2. Introduction:

> The idea of this project is to design and develop a stand-alone, FPGA-based smart camera that can perform the processing tasks such as Sobel, Prewitt, dilation edge detection, color object detection, emboss effects and output the alarm signal in the case of detection to short-range wireless systems using the zigbee.

> With the rapid development of remote sensing camera has become a popular sensor device for monitoring and surveillance systems. It is the first step of video analysis and understanding with remote sensing
video especially the detection of object which is necessary step to extract the information from stream of binary raw data from the sensors. The purpose of the detection is to discover the information about the identified object in the presence of the surrounding objects. The sensor device used is a THDB-D5M, which is five mega pixel digital CMOS color image sensor and it contains a power voltage circuit, a low noise amplifier and clock driver circuit. Its flexibility and ease of use makes it a good choice for the system.

> The raw data of color video stream and edge detection is very large, so speed of video processing is a difficult problem. Therefore in order to improve the performance of real time video processing FPGA is an effective device to realize real-time parallel processing of vast amounts of video data. Moreover, adopting FPGA as a development platform than PC and other IC is to perform data intensive video processing tasks with real requirements. Therefore, architecture of detection is designed with a FPGA chip called Cyclone II 2C70, and it can process 800 x 480 x 10 RGB color scale video successfully. This device can locate the detected color object and the edge of the gray frame quickly and efficiently.

3. CMOS Camera D5M:

> The idea behind to use the D5M camera for the FPGA was to have the easy connection of 40 pins between these two devices. This 40 pins connection provide input/output communication using the pixel clock, pixel data (12 bits), power (3.3V),Serial clock, serial data(I2C),frame valid and line valid.

> A typical camera system is shown in figure 1. At the heart of every digital camera is an image sensor either CCD image senor or a CMOS sensor. Both types of sensor capture the light through the lens and convert into the electrical signal which is further processed by ADC. Nowadays, majority of sensors consist of high performance ADC converters which are employed to produce the digital output. Most CMOS image sensors have ADC resolutions of 10 to 12 bits. In this project, D5M camera has 12 bits ADC resolution. The D5M pixel array consists a 2752-coloumn by 2004-row matrix. The pixel array is addressed by column and row. The array consists of a 2592-column by 1944-row active region and a border region as shown below.

> The output images are divided into frames, which are further divided into lines. The output signals frame valid and lines valid are used to indicate the boundaries between the lines and frames [3]. Pixel clock is used as a clock to latch the data. For each pixel clock cycle, one 12-bit pixel data outputs on the data out pins [3]. When both frame valid and line valid are asserted, the pixel is valid. Pixel clock cycles that occur when frame valid is negated are called vertical blanking. Pixel clock cycles that occur when only line
valid is negated are called horizontal blanking. The camera has an array of 255 register, a lot of them are configurable, and it is possible to set up the operation of the camera by writing to these registers. This communication is performed using a generic two wire serial interface commonly referred to as I2C[3]. There are two different communication modes, control / configuration mode which included read/write values to the register in the D5M card, and pixel data read out which consists of reading the pixel data from the camera card [3].
