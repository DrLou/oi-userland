#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"). You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

# 
# Copyright 2013, Adam Stevko. All rights reserved.
#

include ../../make-rules/shared-macros.mk

COMPONENT_NAME=		tuntap
COMPONENT_VERSION=	1.3.2
COMPONENT_LICENSE=	GPLv2
COMPONENT_GIT_REV=	43816b1
COMPONENT_SRC=		kaizawa-$(COMPONENT_NAME)-$(COMPONENT_GIT_REV)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	sha256:6ed84336b3eaf29aa227bfc0b5a6e7143431862b97113a31c20b05ba50c0ca44
COMPONENT_PROJECT_URL=	http://www.whiteboard.ne.jp/~admin2/tuntap/
COMPONENT_ARCHIVE_URL= 	https://codeload.github.com/kaizawa/tuntap/legacy.tar.gz/$(COMPONENT_GIT_REV)

COMPONENT_DESCRIPTION=	tuntap is a Virtual Point-to-Point network device: \
a TAP driver for OpenIndiana that can be used for \
OpenVPN, OpenConnect, and vpnc. The code is based on the \
Universal TUN/TAP driver. Some changes were made and code added \
for supporting Ethernet tunneling feature, since the Universal \
TUN/TAP driver for Solaris only supports IP tunneling known as TUN.

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

PKG_OPTIONS +=		-D COMPONENT_DESCRIPTION="$(COMPONENT_DESCRIPTION)"

PATCH_LEVEL = 0

CFLAGS +=	$(CPP_LARGEFILES)
LDFLAGS +=	$(LD_Z_DEFS) $(LD_Z_TEXT) -lpthread

CONFIGURE_OPTIONS.32 +=  --disable-64bit
CONFIGURE_OPTIONS.64 +=  --enable-64bit

PKGLINT=true

# common targets
build:          $(BUILD_32_and_64)

install:	$(INSTALL_32_and_64)

BUILD_PKG_DEPENDENCIES =	$(BUILD_TOOLS)

include $(WS_TOP)/make-rules/depend.mk
