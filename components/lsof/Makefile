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
# Copyright 2016 Jim Klimov. All rights reserved.
#

include ../../make-rules/shared-macros.mk

COMPONENT_NAME=		lsof
COMPONENT_VERSION=	4.89
COMPONENT_PROJECT_URL=	http://freecode.com/projects/util-linux
COMPONENT_SUMMARY=	LSOF - lister of opened files
COMPONENT_SRC=		$(COMPONENT_NAME)_$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.bz2
# Theoretical upstream is ftp://lsof.itap.purdue.edu/pub/tools/unix/lsof
# but it is not available at the time of this writing
COMPONENT_ARCHIVE_URL=	ftp://sunsite.ualberta.ca/pub/Mirror/$(COMPONENT_NAME)/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH=	\
    sha256:81ac2fc5fdc944793baf41a14002b6deb5a29096b387744e28f8c30a360a3718

include ../../make-rules/prep.mk
include ../../make-rules/justmake.mk
include ../../make-rules/ips.mk

# Snatched from espeak component
BINDIR.32=/usr/bin
BINDIR.64=/usr/bin/$(MACH64)

LIBDIR.32=/usr/lib
LIBDIR.64=/usr/lib/$(MACH64)

COMPONENT_COMMON_ARGS += -C $(BUILD_DIR_$(BITS))
COMPONENT_COMMON_ARGS += BINDIR=$(BINDIR.$(BITS))
COMPONENT_COMMON_ARGS += LIBDIR=$(LIBDIR.$(BITS))

COMPONENT_COMMON_ENV += CC=$(CC)
COMPONENT_COMMON_ENV += CXX=$(CXX)
COMPONENT_COMMON_ENV += CXXFLAGS="$(CXXFLAGS)"
COMPONENT_COMMON_ENV += LDFLAGS="$(LDFLAGS)"

COMPONENT_BUILD_ARGS += $(COMPONENT_COMMON_ARGS)
COMPONENT_BUILD_ENV += $(COMPONENT_COMMON_ENV)
COMPONENT_INSTALL_ARGS += $(COMPONENT_COMMON_ARGS)
COMPONENT_INSTALL_ENV += $(COMPONENT_COMMON_ENV)

COMPONENT_PREP_ACTION = \
    ( cd $(SOURCE_DIR) && tar xf - < $(COMPONENT_SRC)_src.tar )

COMPONENT_PRE_BUILD_ACTION = \
    ( cd $(@D) && cp -prf "$(SOURCE_DIR)/$(COMPONENT_SRC)_src"/./ ./ && \
      yes '' | SOLARIS_KERNBITS=$(BITS) ./Configure solaris )

build:		$(BUILD_32_and_64)

# The p5m manifest directly pulls from source dirs (the "make install" action
# for Solaris in LSOF sources only prints hints what/how should be set up)
install:	$(INSTALL_32_and_64)

test:		$(NO_TESTS)

include ../../make-rules/depend.mk
