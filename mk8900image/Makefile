MKIMAGEOBJS=mk8900image.o
LIBRARIES=-L/usr/lib -lm -ldl -lpng -lcrypto -lz
CFLAGS +=
UNAME := $(shell uname -s)

LIBXPWN=libxpwn.a

%.o:	%.c
	@echo "Compiling $@"
	@$(CC) $(CFLAGS) -c $< -o $@

mk8900image:	$(MKIMAGEOBJS)
	@echo "Building $@"
	@$(CC) $(CFLAGS) $(MKIMAGEOBJS) $(LIBXPWN) $(LIBRARIES) -o $@

clean:
	@rm -f *.o
	@rm -f mk8900image
