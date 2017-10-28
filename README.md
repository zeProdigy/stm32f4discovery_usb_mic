# stm32f4discovery_usb_mic
USB микрофон на базе отладочной платы stm32f4discovery с использованием libopencm3

## Сборка
```
mkdir build && cd build
cmake .. -DCMAKE_TOOLCHAIN_FILE=../toolchain.cmake
make
```
