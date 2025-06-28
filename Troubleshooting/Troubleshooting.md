\# The Current Issue: Trackers Connect But There is no Data

The SlimeVR server is not able to get any orientation data from the ICM-45686. Everything seems to indicate everything is okay except for the lack of data.

!\[Slime UI](https://raw.githubusercontent.com/rkeen9/Bert-Slime-Tracker/refs/heads/main/Troubleshooting/slimeUI.png)

!\[Device Info|215](https://raw.githubusercontent.com/rkeen9/Bert-Slime-Tracker/refs/heads/main/Troubleshooting/Tracker-Info.png)



When looking in the serial log, all the I2C sensors look to be getting detected as well:

!\[Serial Log](https://raw.githubusercontent.com/rkeen9/Bert-Slime-Tracker/refs/heads/main/Troubleshooting/serial-log.png)



The "Sensor\[1]" errors I'm assuming are because I don't have a secondary IMU connected.



\# Testing

We know that the issue is that the SlimeVR server is not able to receive any data from the ICM-45586. This makes the number one suspect the I2C connection. To isolate this I uploaded some sample code from the ICM45686 Arduino library to my D1 Mini. This code was as follows:

```

\#include "ICM45686.h"



// Instantiate an ICM456XX with LSB address set to 0

ICM456xx IMU(Wire,0);



void setup() {

&nbsp; int ret;

&nbsp; Serial.begin(115200);

&nbsp; while(!Serial) {}



&nbsp; // Initializing the ICM456XX

&nbsp; ret = IMU.begin();

&nbsp; if (ret != 0) {

&nbsp;   Serial.print("ICM456xx initialization failed: ");

&nbsp;   Serial.println(ret);

&nbsp;   while(1);

&nbsp; }

&nbsp; // Accel ODR = 100 Hz and Full Scale Range = 16G

&nbsp; IMU.startAccel(100,16);

&nbsp; // Gyro ODR = 100 Hz and Full Scale Range = 2000 dps

&nbsp; IMU.startGyro(100,2000);

&nbsp; // Wait IMU to start

&nbsp; delay(100);

}



void loop() {



&nbsp; inv\_imu\_sensor\_data\_t imu\_data;



&nbsp; // Read registers

&nbsp; IMU.getDataFromRegisters(imu\_data);



&nbsp; // Format data for Serial Plotter

&nbsp; Serial.print("AccelX:");

&nbsp; Serial.println(imu\_data.accel\_data\[0]);

&nbsp; Serial.print("AccelY:");

&nbsp; Serial.println(imu\_data.accel\_data\[1]);

&nbsp; Serial.print("AccelZ:");

&nbsp; Serial.println(imu\_data.accel\_data\[2]);

&nbsp; Serial.print("GyroX:");

&nbsp; Serial.println(imu\_data.gyro\_data\[0]);

&nbsp; Serial.print("GyroY:");

&nbsp; Serial.println(imu\_data.gyro\_data\[1]);

&nbsp; Serial.print("GyroZ:");

&nbsp; Serial.println(imu\_data.gyro\_data\[2]);

&nbsp; Serial.print("Temperature:");

&nbsp; Serial.println((imu\_data.temp\_data/128)+25);



&nbsp; delay(100);

}

```



The only change was modifying the temperature line to get a value is Celsius based on this formula from the datasheet

!\[Temp Formula](https://raw.githubusercontent.com/rkeen9/Bert-Slime-Tracker/refs/heads/main/Troubleshooting/temperature\_formula.png)

This was the result:

!\[Rotation Gif](https://raw.githubusercontent.com/rkeen9/Bert-Slime-Tracker/refs/heads/main/Troubleshooting/rotation-test.gif)

It is hard to interpret but the data seems right. Rotating about the Y-axis resulted in most of the change being in the GyroY value (orange line). And since these values are angular rotation rate, all of the rotational values went close to 0 when holding the sensor still.



An easier to follow test is shown below. In this test, I only show the temperature reading and briefly hit the sensor with a heat gun set to its lowest setting. 

!\[temp](https://raw.githubusercontent.com/rkeen9/Bert-Slime-Tracker/refs/heads/main/Troubleshooting/I2C-Test.gif)

You can see that the temperature value reacts as expected when heated up and returns as the sensor cools down.



With these results, I'm not sure whether the I2C interface is the issue. 





