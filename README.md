# STM32-disc-mpu6050

This project would help you to get sensor data from MPU6050.

When the data ready, INT Pin will be latched(active high).
In the while loop, you will constantly check INT Pin status.
And if INT Pin latched, you will get 6 axis data from register.

Start and initialize the I2C bus.

![I2C setting](./img/I2C%20setting.PNG)

Also activate GPIO_Input at PB5 Pin.

![GPIO setting](./img/gpio%20setting.PNG)

Copy the (MPU6050.c, MPU6050.h) to (Src, Inc) respectively.

In the main.c file, include header file.
```
/* USER CODE BEGIN Includes */
#include "MPU6050.h"
/* USER CODE END Includes */
```

Initialize MPU6050 sensor inside of int main(void) function.
  ```
  /* USER CODE BEGIN 2 */
	if(MPU6050_Initialization() == 1)
	{
		while(1)
		{
			HAL_GPIO_TogglePin(LED_BLUE_PORT, LED_BLUE_PIN);
			HAL_Delay(100);
		}
	}
  /* USER CODE END 2 */
  ```
 
Get sensor data when the data is ready.
```
	while (1)
	{
    /* USER CODE END WHILE */
    /* USER CODE BEGIN 3 */
		if(MPU6050_DataReady() == 1)
		{
			MPU6050_Get6AxisRawData(&MPU6050);
			MPU6050_DATA_CONVERT(&MPU6050);
//			printf("%f, %f, %f\n", MPU6050.acc_x, MPU6050.acc_y, MPU6050.acc_z);
			printf("%f, %f, %f\n", MPU6050.gyro_x, MPU6050.gyro_y, MPU6050.gyro_z);
//			printf("%d, %d, %d\n", MPU6050.acc_x_raw, MPU6050.acc_y_raw, MPU6050.acc_z_raw);
		}
	}
  /* USER CODE END 3 */
}
```

you can get sensor data like this.

![sensor data](./img/sensor%20data.PNG)
  
