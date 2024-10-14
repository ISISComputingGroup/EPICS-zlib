TOP=../..

include $(TOP)/configure/CONFIG
#----------------------------------------
#  ADD MACRO DEFINITIONS AFTER THIS LINE
#=============================

#==================================================
# build a support library

LIBRARY_IOC += zlib zlibd

# xxxRecord.h will be created from xxxRecord.dbd
#DBDINC += xxxRecord
# install zlib.dbd into <top>/dbd
SRC_DIRS += $(TOP)/zlibApp/src/test
DBD += zlib.dbd
INC += zlib.h zconf.h

zlib_SRCS += adler32.c compress.c crc32.c deflate.c gzclose.c gzlib.c gzread.c \
       gzwrite.c infback.c inffast.c inflate.c inftrees.c trees.c uncompr.c zutil.c
zlib_LDFLAGS_WIN32 += /def:$(TOP)/zlibApp/src/win32/zlib.def

# to help a debug cmake build find zlib
zlibd_SRCS += $(zlib_SRCS)
zlibd_LDFLAGS_WIN32 += $(zlib_LDFLAGS_WIN32)

PROD_IOC += zlib_example
zlib_example_SRCS += example.c
zlib_example_LIBS += zlib


#===========================

include $(TOP)/configure/RULES
#----------------------------------------
#  ADD RULES AFTER THIS LINE

distclean:
	make -f Makefile.in distclean
