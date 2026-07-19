flags :=
cflags :=
ldflags :=

NASMENV="-i include"
export NASMENV

.PHONY: clean run

all: loader.o

loader.img: loader.o
    ld --script=loader.ld $< -o $@
	chmod -x $@
	truncate -s "%512" $@
	rm -f kernel.img
	dd if=/dev/zero of=kernel.img bs=1 count=512


loader.o: loader.asm
	nasm $(flags) $<

clean:
	rm -f *.o *.img

run:
	qqemu-system-i386 -nographics -hda loader.img -hdb kernel.img -m 16M