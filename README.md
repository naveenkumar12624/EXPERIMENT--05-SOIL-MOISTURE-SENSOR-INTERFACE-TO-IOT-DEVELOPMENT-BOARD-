# EXPERIMENT--05-SOIL-MOISTURE-SENSOR-INTERFACE-TO-IOT-DEVELOPMENT-BOARD-
## Aim: To Interface a Analog Input  (soil moisture sensor) to ARM IOT development board and write a  program to obtain  the data on the com port 
## Components required: STM32 CUBE IDE, ARM IOT development board,  STM programmer tool.
## Theory 
#### Hardware Overview
A typical soil moisture sensor consists of two parts.

The Probe
The sensor includes a fork-shaped probe with two exposed conductors that is inserted into the soil or wherever the moisture content is to be measured.

As previously stated, it acts as a variable resistor, with resistance varying according to soil moisture.
![image](https://github.com/vasanthkumarch/EXPERIMENT--05-SOIL-MOISTURE-SENSOR-INTERFACE-TO-IOT-DEVELOPMENT-BOARD-/assets/36288975/00e1751d-44e6-41e3-b261-717a657861be)
The Module
In addition, the sensor includes an electronic module that connects the probe to the Arduino.

The module generates an output voltage based on the resistance of the probe, which is available at an Analog Output (AO) pin.

The same signal is fed to an LM393 High Precision Comparator, which digitizes it and makes it available at a Digital Output (DO) pin.

![image](https://github.com/vasanthkumarch/EXPERIMENT--05-SOIL-MOISTURE-SENSOR-INTERFACE-TO-IOT-DEVELOPMENT-BOARD-/assets/36288975/85f21aed-ce9b-416c-8ad2-d0919eb32dbf)
The module includes a potentiometer for adjusting the sensitivity of the digital output (DO).

You can use it to set a threshold, so that when the soil moisture level exceeds the threshold, the module outputs LOW otherwise HIGH.

This setup is very useful for triggering an action when a certain threshold is reached. For example, if the moisture level in the soil exceeds a certain threshold, you can activate a relay to start watering the plant.


Soil Moisture Sensor Pinout
The soil moisture sensor is extremely simple to use and only requires four pins to connect.

soil moisture sensor pinout
AO (Analog Output) generates analog output voltage proportional to the soil moisture level, so a higher level results in a higher voltage and a lower level results in a lower voltage.

DO (Digital Output) indicates whether the soil moisture level is within the limit. D0 becomes LOW when the moisture level exceeds the threshold value (as set by the potentiometer), and HIGH otherwise.

VCC supplies power to the sensor. It is recommended that the sensor be powered from 3.3V to 5V. Please keep in mind that the analog output will vary depending on the voltage supplied to the sensor.

GND is the ground pin.

![image](https://github.com/vasanthkumarch/EXPERIMENT--05-SOIL-MOISTURE-SENSOR-INTERFACE-TO-IOT-DEVELOPMENT-BOARD-/assets/36288975/bf4f99ab-6c72-4d9b-9e65-40669401ce04)

## Procedure:
 1. click on STM 32 CUBE IDE, the following screen will appear 
 ![image](https://user-images.githubusercontent.com/36288975/226189166-ac10578c-c059-40e7-8b80-9f84f64bf088.png)

 2. click on FILE, click on new stm 32 project 
 ![image](https://user-images.githubusercontent.com/36288975/226189215-2d13ebfb-507f-44fc-b772-02232e97c0e3.png)
![image](https://user-images.githubusercontent.com/36288975/226189230-bf2d90dd-9695-4aaf-b2a6-6d66454e81fc.png)
3. select the target to be programmed  as shown below and click on next 

![image](https://user-images.githubusercontent.com/36288975/226189280-ed5dcf1d-dd8d-43ae-815d-491085f4863b.png)

4.select the program name 
![image](https://user-images.githubusercontent.com/36288975/226189316-09832a30-4d1a-4d4f-b8ad-2dc28f137711.png)


5. corresponding ioc file will be generated automatically 
![image](https://user-images.githubusercontent.com/36288975/226189378-3abbdee2-0df6-470f-a3cd-79c74e3d3ad8.png)

6.select the appropriate pins as gipo, in or out, USART or required options and configure 
![image](https://user-images.githubusercontent.com/36288975/226189403-f7179f1a-3eae-4637-826b-ab4ec35ba1e1.png)
![image](https://user-images.githubusercontent.com/36288975/226189425-2b2414ce-49b3-4b61-a260-c658cb2e4152.png)


7.click on cntrl+S , automaticall C program will be generated 
![image](https://user-images.githubusercontent.com/36288975/226189443-8b43451d-0b14-47e4-a20b-cc09c6ad8458.png)
![image](https://user-images.githubusercontent.com/36288975/226189450-85ffa969-2ffb-4788-81e5-72d60fdda0f1.png)
8. edit the program and as per required 
![image](https://user-images.githubusercontent.com/36288975/226189461-a573e62f-a109-4631-a250-a20925758fe0.png)

9. use project and build all 
![image](https://user-images.githubusercontent.com/36288975/226189554-3f7101ac-3f41-48fc-abc7-480bd6218dec.png)
10. once the project is bulild 
![image](https://user-images.githubusercontent.com/36288975/226189577-c61cc1eb-3990-4968-8aa6-aefffc766b70.png)

11. click on debug option 
![image](https://user-images.githubusercontent.com/36288975/226189625-37daa9a3-62e9-42b5-a5ce-2ac63345905b.png)

12. connect the  iot board to power supply and usb 

13. After connecting open the STM cube programmer 
![image](https://user-images.githubusercontent.com/36288975/227599356-9c465b7e-6bd0-436b-b4e8-742ed25e06ce.png)

14. click on UART and click on connect 
![image](https://user-images.githubusercontent.com/36288975/227599458-26976d4a-f2d4-49f0-a49f-31f46eb15761.png)

15. once it is connected , click on Erasing and programming option 
![image](https://user-images.githubusercontent.com/36288975/227599531-f03d277e-440f-4f8a-8875-97f8e8058c71.png)

16. flash the bin or hex file as shown below by switching the switch to flash mode 

![image](https://user-images.githubusercontent.com/36288975/227599656-dc4a635f-b5f1-44c8-84c5-ee0a592fa184.png)


17. check for execution of the output by switching the board to run mode 
18. open serial port utility and select appropritate com port, run and verify the reuslts of moisture content .


## STM 32 CUBE PROGRAM :
~~~
#include "main.h"

#include "stdio.h"

void HAL_GPIO_EXTI_Callback(uint16_t);

UART_HandleTypeDef huart2;

void SystemClock_Config(void);

static void MX_GPIO_Init(void);

static void MX_USART2_UART_Init(void);

int main(void) {

SystemClock_Config();

MX_GPIO_Init(); MX_USART2_UART_Init();

while (1) {

  HAL_GPIO_EXTI_Callback(GPIO_PIN_4);
  
  HAL_Delay(1000);
}

}

void SystemClock_Config(void) { RCC_OscInitTypeDef RCC_OscInitStruct = {0}; RCC_ClkInitTypeDef RCC_ClkInitStruct = {0};

__HAL_PWR_VOLTAGESCALING_CONFIG(PWR_REGULATOR_VOLTAGE_SCALE2);

RCC_OscInitStruct.OscillatorType = RCC_OSCILLATORTYPE_MSI; RCC_OscInitStruct.MSIState = RCC_MSI_ON; RCC_OscInitStruct.MSICalibrationValue = RCC_MSICALIBRATION_DEFAULT; RCC_OscInitStruct.MSIClockRange = RCC_MSIRANGE_6; RCC_OscInitStruct.PLL.PLLState = RCC_PLL_NONE; if (HAL_RCC_OscConfig(&RCC_OscInitStruct) != HAL_OK) { Error_Handler(); }

RCC_ClkInitStruct.ClockType = RCC_CLOCKTYPE_HCLK3|RCC_CLOCKTYPE_HCLK |RCC_CLOCKTYPE_SYSCLK|RCC_CLOCKTYPE_PCLK1 |RCC_CLOCKTYPE_PCLK2;

RCC_ClkInitStruct.SYSCLKSource = RCC_SYSCLKSOURCE_MSI;

RCC_ClkInitStruct.AHBCLKDivider = RCC_SYSCLK_DIV1;

RCC_ClkInitStruct.APB1CLKDivider = RCC_HCLK_DIV1;

RCC_ClkInitStruct.APB2CLKDivider = RCC_HCLK_DIV1;

RCC_ClkInitStruct.AHBCLK3Divider = RCC_SYSCLK_DIV1;

if (HAL_RCC_ClockConfig(&RCC_ClkInitStruct, FLASH_LATENCY_0) != HAL_OK) { Error_Handler(); } }

static void MX_USART2_UART_Init(void) {

huart2.Instance = USART2;

huart2.Init.BaudRate = 115200;

huart2.Init.WordLength = UART_WORDLENGTH_8B;

huart2.Init.StopBits = UART_STOPBITS_1;

huart2.Init.Parity = UART_PARITY_NONE; huart2.Init.Mode = UART_MODE_TX_RX; huart2.Init.HwFlowCtl = UART_HWCONTROL_NONE;

huart2.Init.OverSampling = UART_OVERSAMPLING_16;

huart2.Init.OneBitSampling = UART_ONE_BIT_SAMPLE_DISABLE; huart2.Init.ClockPrescaler = UART_PRESCALER_DIV1; huart2.AdvancedInit.AdvFeatureInit = UART_ADVFEATURE_NO_INIT; if (HAL_UART_Init(&huart2) != HAL_OK) { Error_Handler(); } if (HAL_UARTEx_SetTxFifoThreshold(&huart2, UART_TXFIFO_THRESHOLD_1_8) != HAL_OK) { Error_Handler(); } if (HAL_UARTEx_SetRxFifoThreshold(&huart2, UART_RXFIFO_THRESHOLD_1_8) != HAL_OK) { Error_Handler(); } if (HAL_UARTEx_DisableFifoMode(&huart2) != HAL_OK) { Error_Handler(); }

}

static void MX_GPIO_Init(void) { GPIO_InitTypeDef GPIO_InitStruct = {0};

__HAL_RCC_GPIOA_CLK_ENABLE();

GPIO_InitStruct.Pin = GPIO_PIN_4; GPIO_InitStruct.Mode = GPIO_MODE_IT_FALLING; GPIO_InitStruct.Pull = GPIO_PULLUP; HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);

}

void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin) { if(HAL_GPIO_ReadPin(GPIOA,GPIO_PIN_4)==0) { printf("IR ON\n"); } else { printf("IR Off\n"); } }

PUTCHAR_PROTOTYPE { HAL_UART_Transmit(&huart2, (uint8_t *)&ch,1,0xFFFF);

return ch;
}

void Error_Handler(void) {

__disable_irq(); while (1) { }

}

void assert_failed(uint8_t *file, uint32_t line) {

}
~~~


## Output screen shots on serial monitor   :

![image](https://github.com/SdMdZahi7/EXPERIMENT--05-SOIL-MOISTURE-SENSOR-INTERFACE-TO-IOT-DEVELOPMENT-BOARD-/assets/94187572/956d4ee1-e81b-4566-b7ce-7d8e4f89c702)
![image](https://github.com/SdMdZahi7/EXPERIMENT--05-SOIL-MOISTURE-SENSOR-INTERFACE-TO-IOT-DEVELOPMENT-BOARD-/assets/94187572/f3aa9c00-a70e-4286-b58e-1fa3a095ff0b)

![image](https://github.com/SdMdZahi7/EXPERIMENT--05-SOIL-MOISTURE-SENSOR-INTERFACE-TO-IOT-DEVELOPMENT-BOARD-/assets/94187572/1d9ecf76-9e76-4217-9848-26e6e4f2d37e)
![image](https://github.com/SdMdZahi7/EXPERIMENT--05-SOIL-MOISTURE-SENSOR-INTERFACE-TO-IOT-DEVELOPMENT-BOARD-/assets/94187572/c2f1c620-e28e-440a-b490-898dabdae3cf)

 
 
 
 
## Result :
Interfacing a Analog Input (soil moisture sensor) with ARM microcontroller based IOT development is executed and the results visualized on serial monitor 
