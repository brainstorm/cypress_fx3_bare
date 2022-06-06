all : latencytest

LCYPRIO:=../libcyprio
CFLAGS:=-I$(LCYPRIO) -O1 -g
LDFLAGS:=`pkg-config --libs libusb` -lpthread

CYPRIO:=$(LCYPRIO)/libcyprio.c $(LCYPRIO)/libcyprio_util.c

latencytest : latencytest.c $(CYPRIO)
	gcc -o $@ $^ $(CFLAGS) $(LDFLAGS)

clean :
	rm -rf *.o *~ latencytest
