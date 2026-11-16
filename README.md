# Industrial Computing Lab

Repository per i progetti del laboratorio di *Industrial Computing*.

## Materiale condiviso

Documentazione, slide e altro materiale del progetto sono disponibili nella
[cartella condivisa su Google Drive](https://drive.google.com/drive/folders/1igPAx72EVBoXDN0tzx1DOg6gq03VXlYg?usp=sharing).

## Struttura del repository

| Cartella | Descrizione |
|----------|-------------|
| [`finite_state_machine/`](finite_state_machine) | Firmware per STM32L475 che implementa una macchina a stati finiti |

## finite_state_machine

Progetto generato con STM32CubeMX (`finite_state_machine.ioc`) per il microcontrollore **STM32L475xx**.

- Periferiche configurate: GPIO (LED1), USART1, USART2
- HAL: `STM32L4xx_HAL_Driver` + CMSIS
- Build system: CMake + Ninja, toolchain `arm-none-eabi-gcc`

```
finite_state_machine/
├── Core/         # codice applicativo (main.c, interrupt, init HAL)
├── Drivers/      # CMSIS e driver HAL STM32L4xx
├── cmake/        # toolchain file e integrazione CubeMX
├── CMakeLists.txt
└── CMakePresets.json
```

### Requisiti

- [Arm GNU Toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads) (`arm-none-eabi-gcc`)
- [CMake](https://cmake.org/) ≥ 3.22
- [Ninja](https://ninja-build.org/)
- Un programmatore/debugger (es. ST-Link) per il flash, ad esempio con `openocd` o STM32CubeProgrammer

### Build

```sh
cd finite_state_machine
cmake --preset Debug
cmake --build --preset Debug
```

Per la build ottimizzata usare il preset `Release`. L'output si trova in `build/<preset>/`.

### Modifica della configurazione hardware

Aprire `finite_state_machine.ioc` con STM32CubeMX, modificare i pin/periferiche e rigenerare il codice.
Scrivere il codice personalizzato solo nelle sezioni `USER CODE BEGIN/END`, per non perderlo alla rigenerazione.
