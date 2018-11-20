#---------------------------------------------------------------------------------
.SUFFIXES:
ifeq ($(strip $(DEVKITPPC)),)
$(error "Please set DEVKITPPC in your environment. export DEVKITPPC=<path to>devkitPPC")
endif
include $(DEVKITPPC)/wii_rules
#---------------------------------------------------------------------------------
TARGET	:= IOSInterface
BUILD	:= ../../../data
OUTPUT	:= $(BUILD)/$(TARGET).bin
#---------------------------------------------------------------------------------
CFLAGS	:= -Os -Wall -s -nostartfiles -mhard-float -T link.ld _crt0.o
OCFLAGS	:= -S -O binary
#---------------------------------------------------------------------------------
.PHONY: all clean

all: asm $(OUTPUT)

asm:
	$(CC) -DDEBUG -O1 -Wall -s -nostartfiles -nostdlib -mhard-float -c _crt0.S

$(OUTPUT):
	$(CC) -DDEBUG -O1 -Wall -s -nostartfiles -nostdlib -mhard-float -T link.ld _crt0.o cache.c debug.c sock.c usb.c -o ../../../data/IOSInterface.bin
	$(OBJCOPY) $(OCFLAGS) $@
	
clean:
	@rm -fr $(BUILD)/$(TARGET).bin
