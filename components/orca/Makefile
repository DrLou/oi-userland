##
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL)". You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright (c) 2014 Alexander Pyhalov
# Copyright (c) 2014 Ken Mays
#

include ../../make-rules/shared-macros.mk

COMPONENT_NAME=         orca
COMPONENT_VERSION=      2.32.1
COMPONENT_PROJECT_URL=  http://www.gnome.org
COMPONENT_SUMMARY=      Orca screen reader/magnifier
COMPONENT_SRC=          $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=      $(COMPONENT_SRC).tar.bz2
COMPONENT_ARCHIVE_HASH= \
    sha256:44da9da70c1b47bc87fda8f3b9da4cc1df9993d92388434f5707d39b5a832629
COMPONENT_ARCHIVE_URL=  http://ftp.gnome.org/pub/GNOME/sources/$(COMPONENT_NAME)/2.32/$(COMPONENT_ARCHIVE)


include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

PATH=/usr/gnu/bin:/usr/bin

CONFIGURE_OPTIONS+=	--sysconfdir=/etc

CONFIGURE_ENV+= PYTHON="$(PYTHON)"

# common targets
build:		$(BUILD_32)

install:	$(INSTALL_32)

test:		$(NO_TESTS)

BUILD_PKG_DEPENDENCIES = $(BUILD_TOOLS)

include $(WS_TOP)/make-rules/depend.mk
