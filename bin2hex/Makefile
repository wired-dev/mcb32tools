SRCDIR		= $(shell pwd)
BUILDDIR	= ../build/bin2hex

INCS		+= -I$(SRCDIR)/../build/binutils/bfd
INCS		+= -I$(SRCDIR)/../build/binutils/intl
INCS		+= -I$(SRCDIR)/../downloads/$(BUILD_BINUTILS)/include
INCS		+= -I$(SRCDIR)/../build/binutils/binutils
INCS		+= -I$(SRCDIR)/../downloads/$(BUILD_BINUTILS)/binutils
LIBS		+= $(wildcard $(SRCDIR)/../build/binutils/bfd/*.o)
LIBS		+= $(wildcard $(SRCDIR)/../build/binutils/libiberty/*.o)
LIBS		+= $(wildcard $(SRCDIR)/../build/binutils/intl/*.o)
LIBS		+= $(SRCDIR)/../build/binutils/binutils/bucomm.o
LIBS		+= $(SRCDIR)/../build/binutils/binutils/filemode.o

CFLAGS		= -Wall $(INCS)
LDFLAGS		= -ldl

## Detect Mac OSX
ifneq ($(OS),Windows_NT)
	LDFLAGS += -lz
endif

ifeq ($(shell uname -s),Darwin)
	LDFLAGS += -liconv
endif

$(BUILDDIR)/$(TARGET)-bin2hex: $(BUILDDIR) $(BUILDDIR)/bin2hex.o
	$(CC) -o "$@" "$(BUILDDIR)/bin2hex.o" $(LIBS) $(LDFLAGS)

install:
	install -m 755 "$(BUILDDIR)/$(TARGET)-bin2hex" "$(PREFIX)/bin"

install-strip:
	install -s -m 755 "$(BUILDDIR)/$(TARGET)-bin2hex" "$(PREFIX)/bin"

$(BUILDDIR):
	mkdir -p $@

$(BUILDDIR)/bin2hex.o: $(SRCDIR)/bin2hex.c
	$(CC) $(CFLAGS) -c -o $@ $<
