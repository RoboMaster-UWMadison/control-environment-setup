# led_program
Read as your intro to working with STM32CubeMX and Keil.

## Table of Contents


## Prerequisites
(cubemx setup)[../cubemx-tutorial.md]
(keil setup)[../keil-tutorial.md]
Optional: (github practices)[../github-workflow.md]

## Creating a New Project in CubeMX

Open STM32CubeMX → click File → New Project. Search for STM32F407IG and select the STM32F407IGHx chip.

//Image: screenshot of MCU selector.

Go to System Core → RCC and set High Speed Clock (HSE) to Crystal/Ceramic Resonator.

//Image: RCC configuration screen.

Open Clock Configuration.

Set input frequency to 12 MHz.

Configure PLL multipliers/dividers:

M = 6

N = 168

P = 2

APB1 Prescaler = 4, APB2 Prescaler = 2.

Image: clock tree diagram.

Go to Pinout & Configuration → SYS, set Debug to Serial Wire.

In Project Manager, name your project and choose Toolchain/IDE → MDK-ARM V5.

In Code Generator, check:

“Copy only the necessary library files”

“Generate peripheral initialization as a pair of .c/.h files per peripheral”

Click GENERATE CODE.

💡 Image suggestion: Screenshot of CubeMX project manager before code generation.

4. Opening the Project in Keil

Open the generated Keil project.

Image: Keil project structure, toolbar with build, debug, download buttons.

Basic Keil options:

Output → enable HEX file if needed.

C/C++ → add header file directories.

Debug → select your ST-Link or J-Link programmer.

Flash Download → choose erase mode (usually Erase Full Chip) and enable Reset and Run.

5. Configuring GPIO for LED in CubeMX

Identify LED pins from the schematic: PH10, PH11, PH12.

Image: board schematic snippet with LED pins.

In CubeMX, set these pins as GPIO_Output.

Rename pins for clarity (e.g., LED_R, LED_G, LED_B).

Regenerate code.

6. Writing the LED Control Code

Use the HAL GPIO function:

HAL_GPIO_WritePin(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin, GPIO_PinState PinState);


GPIOx: port (e.g., GPIOH)

GPIO_Pin: pin number (e.g., GPIO_PIN_10)

PinState: GPIO_PIN_SET (high) or GPIO_PIN_RESET (low)

Example (turn all LEDs ON):
// Inside main loop
HAL_GPIO_WritePin(LED_R_GPIO_Port, LED_R_Pin, GPIO_PIN_SET);
HAL_GPIO_WritePin(LED_G_GPIO_Port, LED_G_Pin, GPIO_PIN_SET);
HAL_GPIO_WritePin(LED_B_GPIO_Port, LED_B_Pin, GPIO_PIN_SET);


This outputs high level to all three LED pins → Red + Green + Blue light mix into white.

Image: photo of dev board with white LED lit.