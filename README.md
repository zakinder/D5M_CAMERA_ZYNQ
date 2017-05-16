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

3.2 FPGA Cyclone II:

> An FPGA is a silicon device that consists of millions of transistors connected to perform logic functions. These logic functions are connected in a way that creates hardware implementation of the applications. FPGAs are truly parallel in nature so different processing operations do not have to compete for the same resources [1].Aircraft, automobiles, radar, missiles, medical and computer are just some of the systems that use FPGAs.

> There are two major types of FPGA: SRAM-based and antifuse-based which are supplied by the device vendors (Actel, Altera, Atmel, Lattice, QuickLogic and Xilinx).FPGA have proven faster performance over conventional general purpose processors. Especially for image processing operations, the speed-ups can be increased up to 800 times by exploiting of parallelism and parallel I/O capabilities [2].Edge detection operator like Prewitt is 80 times faster(1.96ms) on Xilinx XV2000E FPGA than on Pentium III (158.08ms) for 512X512 8 bit image[2]. Therefore, considering the parallelism of FPGA, Cyclone II DE2-70 FPGA development board from Altera was chosen for detection application.

3.3 LTM (LCD Touch Panel Module):

> The LTM consists of three major components: LCD touch panel module, AD converter, and 40-pin expansion header. All of the interfaces on the LTM are connected to Altera DE2-70 board via the 40-pin expansion connector. The LCD and touch panel module will take the control signals provided directly from FPGA as input and display images on the LCD panel. Finally, the AD converter will convert the coordinates of the touch point to its corresponding digital data and output to the FPGA via the expansion header [101].

3.4 Clock Issue:

> Timing plays a very important role in interconnecting the devices and modules. In this project, camera runs at 50 MHz and LTM receiving the data at the clock rate of 27MHz.The clock rate of 27 MHz can be generated from the 50MHz oscillator. To generate an update rate of 27 MHz for a digital line by looping timer function set for 1.85 ticks. FPGA main clock frequency is 50 MHz, so that each clock cycle and unit of time is 20 nanoseconds (ns).
27 MHz =0.03703 us=37.03 ns
37.03 ns/ 20 ns per tick = 1.85 ticks
Since we cannot choose specific partial clock cycles we would have to choose 1 clock cycles which is a delay of 20 ns and corresponds to a frequency of 50 MHz .The next lower frequency we could use is 2
ticks or 25 MHz .Using the 50 MHz FPGA clock, we can only update the digital lines at 25 MHz or 50
MHz, but not in between of these frequencies. Therefore, 27 MHz can’t be generated from the 50 MHz
clock oscillator but can generate 25MHz clock. The solution is to use external 27 MHz Oscillator for the
LTM clock.

3.5 Verilog Implementation:

> The software placed in the FPGA is implemented in Verilog. It provides module level simulation and verification which allows is to build the design up from smaller modules. Once the simulation, synthesis and time verification is verified in the Quartus software, then programmer device tool will load the bit file of verilog onto the FPGA using the USB blaster. The process of programming hardware language has to several steps before being loaded onto the FPGA. Figure below shows the basic concept of HDL programming which is used in this project before the project689.bit being loaded to the cyclone II FPGA.


4. Detailed description of functionality:

4.1 CMOS pixel Capture:

> This is the first module inside the FPGA which communicate with camera. It receives the data of 12 bits per pixel at each clock cycle from the cmos camera when the frame valid and line valid are asserted high. Pixel clock (50MHz) is used to latch the data on the rising edge of the clock. In the case of when clear is set, then it captures on the falling edge of the pixel clock. Vertical blank occurs when frame valid is high. However, horizontal blank only occurs when both frames line valid and frame valid are high. In order to pause, restart, snapshot and change the exposure level of the video, certain registers need to be assigned the hex values. These hex values are given in the datasheet of this camera. Setting these values will enable the features and functionality of the camera. These features were enabled by using the I2C bus which has two wires SDA and SCL. SDA is the data line. SCL is the clock line which is used to synchronize all data transfers over the I2C bus. The SCL & SDA lines are connected to the FPGA and the camera on the I2C bus. Once the registers were assigned the values and valid signal are asserted, the camera output the 12
bits data at the maximum data rate of 96Mp/s. Input clock for the camera is 96MHz which gives the maximum data rate but this data rate should be latched at the 50MHz clock.

> Active pixels: 2,592H x 1,944V Pixel size: 2.2μm x 2.2μm
Color filter array RGB Bayer pattern
Full resolution Programmable up to 15 fps Frame rate
VGA (640 x 480) Programmable up to 70 fps
ADC resolution: 12-bit
Pixel dynamic range: 70.1dB SNRMAX: 38.1dB
Supply Power Voltage: 3.3V I/O Voltage: 1.7V～3.1V

4.2 RAW TO RGB:

> This module generates a 36-bit RGB value for three channels by buffering the incoming serial data stream of 12 bits. Serial data enters into the module in a certain order which is stripped out, into three parallel channels only when signal is valid from camera otherwise assigned blank. This order must be maintained during the image processing in the FPGA so that the frame is read properly at the display controller of the LTM. When the frame is displayed on the LTM it would appear as if you are looking at a mirror image.

> Serial data is filtered into bayer RGB pattern values. The code shown below assigns serial buffer data into parallel RGB bayer pattern stream.


4.3 SDRAM Controller:

> To handle high data rate stream and volume, it has to be stored somewhere so image processing can be implemented at slower rate. The solution is to use memory that can support enough capacity and data rate. DE2-70 board provides two SDRAM chips each have a capacity of 256Mbits (32 Mbytes).
Each chip is organized as 4M x 16 bits x 4 banks. All of the signals, except the clock, can be provided by the SDRAM Controller. SDRAM controller is the most important module of this project. Since it handle
to write and read from SDRAM and it operate using 4 FIFO ports sides. Two fifo ports are used to write into SDRAM and other two fifo ports are used read from SDRAM. All signals needed to communicate with a SDRAM controller used for this project are shown in Figure 7.RGB data enters into two write fifo
ports from left side of the SDRAM controller at 50MHz clock rate and then stored into the SDRAM chip. To read from SDRAM chip, two other fifo ports used to read side1 and side 2 at 27 MHz clock rate.

8. Conclusion:

> Overall the results from the project were satisfied. In this paper, we have shown how to create a pixel which is based on color window detector. We elaborated the concept of edge detection using FPGA device. Improvement can be made for the future work with more in depth parallel and pipeline structure using low level programming techniques. Finally, the least the color detection of any range in FPGA chip also inspires more intelligent control of the system in the future. This stand-alone, FPGA-based smart camera is useful in the tracking of a moving object in the factories, worker’s vest, operator position and missing labels on the object.

*** References:

*[1] http://nptel.iitm.ac.in/courses/Webcoursecontents/IIT%20Kharagpur/Embedded%20systems/Pdf/Lesson-20.pdf
*[2] http://ieeexplore.ieee.org/xpl/freeabs_all.jsp?arnumber=5716147
*[3] http://www.secs.oakland.edu/~ganesan/ece576f10project/index_files/Page361.htm
*[4] Quartus FPGA design software, from http://www.altera.com/products/software/quartus-ii/web-edition/qts-we-index.html
*[5] The Synplify solution Synplicity, from http://www.synplicity.com/products/synplifypro/
*[6] Mentor Graphics Modelsim, from http://www.mentor.com/products/fpga/simulation/modelsim
*[7] http://www.digi.com/support/kbase/kbaseresultdetl.jsp?kb=125
