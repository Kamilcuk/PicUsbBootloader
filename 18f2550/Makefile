# USB bootloader for PICs
# Makefile for the PIC 18f2550, creates bootloader.hex
#
# Copyright (C) 2012 Holger Oehm
#
#  Licensed under the Apache License, Version 2.0 (the "License");
#  you may not use this file except in compliance with the License.
#  You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
#  Unless required by applicable law or agreed to in writing, software
#  distributed under the License is distributed on an "AS IS" BASIS,
#  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#  See the License for the specific language governing permissions and
#  limitations under the License.
#
#
# Additional changes by Kamil Cukrowski 2017
#

OBJECTS=$(patsubst %.asm,%.o,$(wildcard *.asm))
ifndef VID
$(warning VID is not defined, you may want to: make VID=04d8 PID=000b )
VID=04d8
endif
ifndef PID
$(warning PID is not defined, you may want to: make VID=04d8 PID=000b )
PID=000b
endif
ifndef PLLDIV
$(warning PLLDIV is not defined, you may want to: make PLLDIV=5 )
PLLDIV=5
endif
$(warning PLLDIV is equal to $(PLLDIV))

all: bootloader.hex example

example:
	make -C example all

bootloader.hex: $(OBJECTS)
	gplink -o bootloader.hex -a inhx32 -m $(OBJECTS)

%.o : %.asm
	gpasm -c -p p18f2550 -r dec -w 2 --define _PLLDIV_=$(PLLDIV) --define VID=0x$(VID) --define PID=0x$(PID) $<

usb.o: descriptor.inc
descriptor.o: descriptor.inc

clean:
	rm -f *.o *.map *.lst *.cod *.hex
	make -C example clean

.PHONY: all example clean
