# 电控组第二次培训作业
- **丁佳睿**
- ***20263009065***
- ## 实现思路
- 芯片选用 STM32F103C8T6；将 PA7、PB0、PB1 三个 GPIO 配置为推挽输出模式，并使用 User Label 功能分别命名为 **LED0、LED1、LED2**；使能 FreeRTOS（CMSIS-RTOS v2），并创建 LED 任务。
- ## 流水灯逻辑
- 在任务的无限循环中，按 500ms 的间隔依次点亮 LED0 → LED1 → LED2，循环往复，形成流水灯效果。
- ## 非阻塞延时原理
- 用FreeROTS中的“osDelay"使任务在等待时进入阻塞态，不占用CPU的运行，从而实现非阻塞延时。
- ## 核心代码
- ‘‘‘  void StartLED0(void *argument)
{
  /* USER CODE BEGIN StartLED0 */
  /* Infinite loop */
  for(;;) {


    HAL_GPIO_WritePin(LED0_GPIO_Port, LED0_Pin, GPIO_PIN_SET);
    HAL_GPIO_WritePin(LED1_GPIO_Port, LED1_Pin, GPIO_PIN_RESET);
    HAL_GPIO_WritePin(LED2_GPIO_Port, LED2_Pin, GPIO_PIN_RESET);
    osDelay(500);

    HAL_GPIO_WritePin(LED0_GPIO_Port, LED0_Pin, GPIO_PIN_RESET);
    HAL_GPIO_WritePin(LED1_GPIO_Port, LED1_Pin, GPIO_PIN_SET);
    HAL_GPIO_WritePin(LED2_GPIO_Port, LED2_Pin, GPIO_PIN_RESET);
    osDelay(500);


    HAL_GPIO_WritePin(LED0_GPIO_Port, LED0_Pin, GPIO_PIN_RESET);
    HAL_GPIO_WritePin(LED1_GPIO_Port, LED1_Pin, GPIO_PIN_RESET);
    HAL_GPIO_WritePin(LED2_GPIO_Port, LED2_Pin, GPIO_PIN_SET);
    osDelay(500);
  }
} ’’’
