all : isotest recstream

LCYPRIO:=../libcyprio
CFLAGS:=-I$(LCYPRIO) -O1 -g
LDFLAGS:=-lusb -lpthread
LDFLAGS+=-L/opt/homebrew/Cellar/libusb-compat/0.1.5_1/lib -lusb
CFLAGS+=-I/opt/homebrew/Cellar/libusb-compat/0.1.5_1/include

CYPRIO:=$(LCYPRIO)/libcyprio.c $(LCYPRIO)/libcyprio_util.c

isotest : teststream.c os_generic.c $(CYPRIO)
	gcc -o $@ $^ $(CFLAGS) $(LDFLAGS)

recstream : recstream.c os_generic.c $(CYPRIO)
	gcc -o $@ $^ $(CFLAGS) $(LDFLAGS)

clean :
	rm -rf *.o *~ isotest recstream

