all : cyprflash

LCYPRIO:=../libcyprio
CFLAGS:=-I$(LCYPRIO) -Os
CFLAGS:=`pkg-config --cflags libusb`
LDFLAGS:=`pkg-config --libs libusb`

CYPRIO:=$(LCYPRIO)/libcyprio.c $(LCYPRIO)/libcyprio_util.c

cyprflash : cyprflash.c $(CYPRIO)
	gcc -o $@ $^ $(CFLAGS) $(LDFLAGS)

clean :
	rm -rf *.o *~ cyprflash

