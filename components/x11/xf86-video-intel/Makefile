#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2015 Alexander Pyhalov
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME= xf86-video-intel
COMPONENT_VERSION= 2.99.917
COMPONENT_REVISION= 1
COMPONENT_SUMMARY= xf86-video-intel - Intel integrated graphics chipset driver for the Xorg X server
COMPONENT_SRC= $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= $(COMPONENT_SRC).tar.bz2
COMPONENT_ARCHIVE_HASH= \
  sha256:00b781eea055582820a123c47b62411bdf6aabf4f03dc0568faec55faf9667c9
COMPONENT_ARCHIVE_URL= \
  http://xorg.freedesktop.org/archive/individual/driver/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL = http://xorg.freedesktop.org

include $(WS_TOP)/make-rules/prep.mk

CONFIGURE_DEFAULT_DIRS = no

include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

PATCH_LEVEL=0

COMPONENT_PREP_ACTION =        ( cd $(@D) && \
                                        libtoolize --automake --copy --force && \
                                        aclocal -Im4 && \
                                        autoheader && \
                                        automake -a -f -c &&\
                                        autoconf )

# Paths to find libraries/modules to link with 

SERVERMOD_SUBDIR.64=/$(MACH64)
SERVERMOD_SUBDIR=$(SERVERMOD_SUBDIR.$(BITS))
X11_SERVERMODS_DIR=/usr/lib/xorg/modules
MESA_XSERVERMODS_DIR=/usr/lib/mesa/modules
X11_SERVERLIBS_DIR=/usr/lib

LDFLAGS += -R/usr/lib/xorg$(SERVERMOD_SUBDIR)

LD_OPTIONS+= \
        -L$(X11_SERVERMODS_DIR)$(SERVERMOD_SUBDIR) \
        -L$(MESA_XSERVERMODS_DIR)/extensions$(SERVERMOD_SUBDIR) \
        -L$(X11_SERVERMODS_DIR)/extensions$(SERVERMOD_SUBDIR) \
        -L$(X11_SERVERLIBS_DIR)$(ARCHLIBSUBDIR) \
        -R$(X11_SERVERMODS_DIR)$(SERVERMOD_SUBDIR) \
        -R$(MESA_XSERVERMODS_DIR)/extensions$(SERVERMOD_SUBDIR) \
        -R$(X11_SERVERMODS_DIR)/extensions$(SERVERMOD_SUBDIR) \
        -R$(X11_SERVERLIBS_DIR)$(SERVERMOD_SUBDIR) \
	-Wl,-M$(COMPONENT_DIR)/mapfile.externs

# Need to override install path for all the modules
DRIVER_DIR=$(X11_SERVERMODS_DIR)/drivers$(SERVERMOD_SUBDIR)
COMPONENT_COMMON_ARGS = ch7017_ladir='$(DRIVER_DIR)' \
        ch7xxx_ladir='$(DRIVER_DIR)' \
        ivch_ladir='$(DRIVER_DIR)' \
        sil164_ladir='$(DRIVER_DIR)' \
        tfp410_ladir='$(DRIVER_DIR)'

CPPFLAGS += -DXF86DRI

CONFIGURE_OPTIONS += --enable-dri
CONFIGURE_OPTIONS += --enable-xvmc
CONFIGURE_OPTIONS += --libdir=$(X11_SERVERLIBS_DIR)$(SERVERMOD_SUBDIR)
CONFIGURE_OPTIONS += --disable-sna 
CONFIGURE_OPTIONS += --enable-uxa
CONFIGURE_OPTIONS += --disable-selective-werror
CONFIGURE_OPTIONS += --disable-silent-rules

CONFIGURE_ENV += CPPFLAGS="$(CPPFLAGS)"

COMPONENT_BUILD_ARGS += $(COMPONENT_COMMON_ARGS)
COMPONENT_INSTALL_ARGS += $(COMPONENT_COMMON_ARGS)

build: $(BUILD_32_and_64)

install: $(INSTALL_32_and_64)
