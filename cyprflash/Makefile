all : cyprflash

LCYPRIO:=../libcyprio
CFLAGS:=-I$(LCYPRIO) -Os
#CFLAGS+=$(pkg-config --cflags libusb-1.0)
#LDFLAGS+=$(pkg-config --libs libusb-1.0)
LDFLAGS+=-L/opt/homebrew/Cellar/libusb-compat/0.1.5_1/lib
#CFLAGS+=-I/opt/homebrew/Cellar/libusb-compat/0.1.5_1/include -I/opt/homebrew/Cellar/libusb/1.0.26/include/libusb-1.0
CFLAGS+=-I/opt/homebrew/Cellar/libusb-compat/0.1.5_1/include

CYPRIO:=$(LCYPRIO)/libcyprio.c $(LCYPRIO)/libcyprio_util.c

cyprflash : cyprflash.c $(CYPRIO)
	clang -o $@ $^ $(CFLAGS) $(LDFLAGS)

clean :
	rm -rf *.o *~ cyprflash