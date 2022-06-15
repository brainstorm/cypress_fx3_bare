all : cyprflash

LCYPRIO:=../libcyprio
CFLAGS:=-I$(LCYPRIO) -Os
# CFLAGS+=$(pkg-config --cflags libusb)
# LDFLAGS+=$(pkg-config --libs libusb)
LDFLAGS+=-L/opt/homebrew/Cellar/libusb-compat/0.1.5_1/lib -lusb
CFLAGS+=-I/opt/homebrew/Cellar/libusb-compat/0.1.5_1/include

CYPRIO:=$(LCYPRIO)/libcyprio.c $(LCYPRIO)/libcyprio_util.c

cyprflash : cyprflash.c $(CYPRIO)
	clang -o $@ $^ $(CFLAGS) $(LDFLAGS)

clean :
	rm -rf *.o *~ cyprflash