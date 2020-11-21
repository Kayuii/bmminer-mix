
ACLOCAL_AMFLAGS = -I m4

JANSSON_CPPFLAGS= -I$(top_builddir)/compat/jansson-2.9/src -I$(top_srcdir)/compat/jansson-2.9/src

if WANT_USBUTILS
USBUTILS_CPPFLAGS = `pkg-config libusb-1.0 --libs --cflags`
else
USBUTILS_CPPFLAGS =
endif

if STATIC_CURL
LIBCURL_CPPFLAGS = -DCURL_STATICLIB
else
LIBCURL_CPPFLAGS =
endif


EXTRA_DIST	= example.conf linux-usb-cgminer \
		  api-example.php miner.php	\
		  API.class API.java api-example.c windows-build.txt \
		  bitstreams/README API-README FPGA-README \
		  bitforce-firmware-flash.c hexdump.c ASIC-README \
		  01-cgminer.rules

SUBDIRS		= lib compat ccan

bmminer_CPPFLAGS = $(PTHREAD_FLAGS) -fno-strict-aliasing $(JANSSON_CPPFLAGS) $(USBUTILS_CPPFLAGS) $(LIBCURL_CPPFLAGS)

bin_PROGRAMS	= bmminer

bmminer_LDFLAGS	= $(PTHREAD_FLAGS)
bmminer_LDADD	= $(DLOPEN_FLAGS) @LIBCURL_LIBS@ @JANSSON_LIBS@ @LIBZ_LIBS@ @PTHREAD_LIBS@ \
		  @NCURSES_LIBS@ @PDCURSES_LIBS@ @WS2_LIBS@ \
		  @LIBUSB_LIBS@ @MM_LIBS@ @RT_LIBS@ \
		  @MATH_LIBS@ lib/libgnu.a ccan/libccan.a 

bmminer_CPPFLAGS += -I$(top_builddir)/lib -I$(top_srcdir)/lib

if !HAVE_WINDOWS
bmminer_CPPFLAGS += @LIBCURL_CFLAGS@
endif

# common sources
bmminer_SOURCES := cgminer.c

bmminer_SOURCES	+= elist.h miner.h compat.h bench_block.h	\
		   util.c util.h uthash.h logging.h		\
		   sha2.c sha2.h api.c

bmminer_SOURCES	+= logging.c

bmminer_SOURCES	+= klist.h klist.c

bmminer_SOURCES	+= noncedup.c


if WANT_USBUTILS
bmminer_SOURCES += usbutils.c usbutils.h
endif


if WANT_CRC16
bmminer_SOURCES += crc16.c crc.h
endif

# Device drivers

# if HAS_BITMAIN
# bmminer_SOURCES += driver-bitmain.c driver-bitmain.h
# endif

if HAS_BITMAIN_C5
bmminer_SOURCES += driver-btm-c5.c driver-btm-c5.h sha2_c5.c sha2_c5.h
bmminer_SOURCES += clement-bitmain.c clement-bitmain.h
endif

