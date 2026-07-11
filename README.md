[![Version: 1.0 Release](https://img.shields.io/badge/Version-1.0%20Release-green.svg)](https://github.com/0x007e/hal-avr-mega-twi) ![Release](https://github.com/0x007e/hal-avr-mega-twi/actions/workflows/release.yml/badge.svg) [![License GPLv3](https://img.shields.io/badge/License-GPLv3-lightgrey)](https://www.gnu.org/licenses/gpl-3.0.html)

# `hal-avr-mega-twi` - AVR ATmega TWI Hardware Abstraction

The `hal-avr-mega-twi` is a lightweight `twi` hardware abstraction library for AVR `ATmega16A` microcontrollers. It provides a clean interface for `twi` initialization and communication while hiding direct register-level interaction from higher software layers. The library is intended for projects that want to separate low-level device startup code from application logic and establish a small, reusable system layer for AVR targets.

## Features

- `TWI` master configuration for AVR `ATmega16A` devices.
- `TWI` master communication for AVR `ATmega16A` devices.
- Encapsulation of low-level register access.
- Compact and reusable API for embedded projects.
- Foundation for layered HAL architectures.

> The `hal-avr-mega-twi` library reduces coupling by providing a focused interface for essential `twi` system services. This improves portability inside a project, keeps startup code organized, and makes higher-level modules easier to maintain.

## File Structure

![File Structure](https://0x007e.github.io/hal-avr-mega-twi/twi_8c__incl.png)

```
hal/
├── common/
|   ├── defines/
|   |   └── TWI_defines.h
|   └── enums/
|       └── TWI_enums.h
└── avr/
    └── twi/
        ├── twi.c
        └── twi.h
```

## Downloads

The library can be downloaded (`zip` or `tar`), cloned or used as submodule in a project.

| Type      | File               | Description              |
|:---------:|:------------------:|:-------------------------|
| Library   | [zip](https://github.com/0x007E/hal-avr-mega-twi/releases/latest/download/library.zip) / [tar](https://github.com/0x007E/hal-avr-mega-twi/releases/latest/download/library.tar.gz) | AVR ATmega16A `twi` library |

### Using with `git clone`

```sh
mkdir -p ./hal/
git clone https://github.com/0x007E/hal-common.git ./hal
mv ./hal/hal-common ./hal/common

mkdir -p ./hal/avr
git clone https://github.com/0x007E/hal-avr-mega-twi.git ./hal/avr
mv ./hal/avr/hal-avr-mega-twi ./hal/avr/twi
```

### Using as `git submodule`

```sh
git submodule add https://github.com/0x007E/hal-common.git   ./hal/common
git submodule add https://github.com/0x007E/hal-avr-mega-twi.git ./hal/avr/twi
```

## Programming

Additional parameters like peripheral and twi clock speed, prescaler, port multiplexing and many more can be setup in the [header file](./twi.h). A user friendly description can be found [here](https://0x007e.github.io/hal-avr-mega-twi/twi_8h.html).

```c
#include "../hal/avr/twi/twi.h"

int main(void)
{
	twi_init();

    while (1)
    {
        TWI_Error error = TWI_None;

        // TWI-WRITE command
        twi_start();
	
        error |= twi_address(high_byte, TWI_Write);
        error |= twi_set(middle_byte);
        error |= twi_set(low_byte);

        twi_stop();

        // TWI-READ command
        twi_start();
	
        error |= twi_address(high_byte, TWI_Read);
        error |= twi_get(data, TWI_ACK);
        error |= twi_get(data, TWI_NACK);

        twi_stop();
    }
}
```

## Additional Information

| Type       | Link               | Description              |
|:----------:|:------------------:|:-------------------------|
| AVR-Series | [pdf](https://ww1.microchip.com/downloads/en/devicedoc/atmel-8154-8-bit-avr-atmega16a_datasheet.pdf) | ATmega16A datasheet |

---

R. GAECHTER