TOP=../..

include $(TOP)/configure/CONFIG
#----------------------------------------
#  ADD MACRO DEFINITIONS AFTER THIS LINE
#=============================

#==================================================
# build a support library

LIBRARY_IOC += zlib

# xxxRecord.h will be created from xxxRecord.dbd
#DBDINC += xxxRecord
# install zlib.dbd into <top>/dbd
DBD += zlib.dbd
INC += zlib.h zconf.h
USR_LDFLAGS_WIN32 += /def:$(TOP)/zlibApp/src/win32/zlib.def

# specify all source files to be compiled and added to the library
zlib_SRCS += adler32.c compress.c crc32.c deflate.c gzclose.c gzlib.c gzread.c \
       gzwrite.c infback.c inffast.c inflate.c inftrees.c trees.c uncompr.c zutil.c

zlib_LIBS += $(EPICS_BASE_IOC_LIBS)

#===========================

include $(TOP)/configure/RULES
#----------------------------------------
#  ADD RULES AFTER THIS LINE

