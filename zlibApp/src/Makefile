TOP = ../..
include $(TOP)/configure/CONFIG

## setting MAKEFLAGS causes cmake issues
override MAKEFLAGS=

CMAKE ?= cmake

# extract visual studio major version number from path
# unfortunately cannot use %.% so using %.0 but may not match minor version number changes e.g. 10.1
ifneq ($(VisualStudioVersion),)
VS_VERS=$(filter %.0,$(subst \, ,$(VisualStudioVersion)))
else
VS_VERS=$(filter %.0,$(subst \, ,$(VSINSTALLDIR)))
endif
VS_MAJOR=$(word 1,$(subst ., ,$(VS_VERS)))


INSTALL_DIR=$(abspath $(TOP)/install/$(EPICS_HOST_ARCH))
CMAKE_CONFIG_FLAGS=-DCMAKE_INSTALL_PREFIX=$(INSTALL_DIR)
CMAKE_BUILD_FLAGS=
ifneq ($(findstring linux,$(EPICS_HOST_ARCH)),)
CMAKE_GENERATOR=Unix Makefiles
else
ifneq ($(findstring windows,$(EPICS_HOST_ARCH)),)
VS_ARCH=$(VS_MAJOR)
PLATFORM=x64
else
VS_ARCH=$(VS_MAJOR)
PLATFORM=Win32
endif
CMAKE_GENERATOR=Visual Studio $(VS_ARCH)
endif
ifneq ($(findstring debug,$(EPICS_HOST_ARCH)),)
CMAKE_CONFIG_FLAGS += -DCMAKE_BUILD_TYPE:STRING=Debug -DZLIB_BUILD_EXAMPLES:BOOL=OFF
CMAKE_CONFIG=Debug
else
CMAKE_CONFIG=RelWithDebInfo
endif

include $(TOP)/configure/RULES
#----------------------------------------
#  ADD RULES AFTER THIS LINE

ifdef T_A
install:
	$(CMAKE) .. -G "$(CMAKE_GENERATOR)" -A "$(PLATFORM)" -DCMAKE_INSTALL_PREFIX:PATH="$(INSTALL_DIR)" $(CMAKE_CONFIG_FLAGS)
	$(CMAKE) --build . --target install --config $(CMAKE_CONFIG) $(CMAKE_BUILD_FLAGS)
	-$(MKDIR) $(TOP)/bin
	-$(MKDIR) $(TOP)/bin/$(EPICS_HOST_ARCH)
	-$(MKDIR) $(TOP)/lib
	-$(MKDIR) $(TOP)/lib/$(EPICS_HOST_ARCH)
	-$(MKDIR) $(TOP)/include
	$(CP) -f $(INSTALL_DIR)/include/*.h* $(TOP)/include/
	$(CP) -f $(INSTALL_DIR)/bin/* $(TOP)/bin/$(EPICS_HOST_ARCH)/
	$(CP) -f $(INSTALL_DIR)/lib/* $(TOP)/lib/$(EPICS_HOST_ARCH)/
	$(CP) -f $(CMAKE_CONFIG)/zlib*.pdb $(TOP)/bin/$(EPICS_HOST_ARCH)/
# copy zlibd to zlib so we can use zlib.lib in all epics files
# correct dll will be loaded at runtime as name embeded in .lib
ifneq ($(findstring debug,$(EPICS_HOST_ARCH)),)
	$(CP) -f $(INSTALL_DIR)/lib/zlibd.lib $(TOP)/lib/$(EPICS_HOST_ARCH)/zlib.lib
endif
endif
