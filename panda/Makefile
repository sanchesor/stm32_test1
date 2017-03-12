##################################
# stm32 minimal example Makefile
##################################


CC = arm-eabi-gcc
LD = arm-eabi-ld
CP = arm-eabi-objcopy
 
LKR_SCRIPT = stm32_minimal.ld
 
CFLAGS  = -c -fno-common -O0 -g -mcpu=cortex-m3 -mthumb
LFLAGS  = -nostartfiles -T$(LKR_SCRIPT)
CPFLAGS = -Obinary
 
all: main.bin
 
main.o: main.c
	$(CC) $(CFLAGS) -o main.o main.c
 
main.elf: main.o
	$(LD) $(LFLAGS) -o main.elf main.o
 
main.bin: main.elf
	$(CP) $(CPFLAGS) main.elf main.bin
 
clean:
	del *.o *.elf *.bin
 
#IMAGE = test3blink.bin
IMAGE = test3blink.elf
#IMAGE = main.elf
OPENOCD_DIR = C:\Program Files\OpenOCD-20160901\bin
write: 
	 "$(OPENOCD_DIR)\openocd.exe" -f "stlink-v2.cfg" -f "stm32f1x.cfg" -c init -c "reset halt" -c "flash write_image erase $(IMAGE)" -c "verify_image $(IMAGE)" -c "reset" -c shutdown
	 
#	 openocd -f ${OPENOCD_CFG} -c init -c "reset halt" -c "flash write_image erase ${BIN_IMAGE}" -c "verify_image ${BIN_IMAGE}" -c reset -c shutdown