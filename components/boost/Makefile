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
# Copyright 2014 Alexander Pyhalov.  All rights reserved.
# Copyright 2015 Aurelien Larcher. All rights reserved.
#

include ../../make-rules/shared-macros.mk

COMPONENT_NAME=		boost
COMPONENT_VERSION=	1.58.0
COMPONENT_REVISION=	4
COMPONENT_FMRI=		system/library/boost
COMPONENT_CLASSIFICATION=System/Libraries
COMPONENT_SUMMARY=	boost - free peer-reviewed portable C++ source libraries
COMPONENT_SRC=		$(COMPONENT_NAME)_1_58_0
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.bz2
COMPONENT_ARCHIVE_HASH= \
  sha256:fdfc204fc33ec79c99b9a74944c3e54bd78be4f7f15e260c0e2700a36dc7d3e5
COMPONENT_ARCHIVE_URL= \
  http://sourceforge.net/projects/boost/files/boost/$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)/download
COMPONENT_PROJECT_URL=	http://www.boost.org
COMPONENT_LICENSE_FILE=	boost.license
COMPONENT_LICENSE=	Boost Software license

include ../../make-rules/prep.mk
include ../../make-rules/ips.mk
include ../../make-rules/modules.mk

LIBDIR.32= $(USRLIBDIR)
LIBDIR.64= $(USRLIBDIR64)
LIBDIR= $(LIBDIR.$(BITS))

DOCDIR=$(USRSHAREDOCDIR)/$(COMPONENT_NAME)-$(COMPONENT_VERSION)

GTAR=$(GNUBIN)/tar
BJAM=./bjam --v2 -d+2 -q address-model=$(BITS) \
	-sBUILD="release <threading>single/multi" \
	--prefix=$(PROTO_DIR)$(USRDIR) \
	--libdir=$(PROTO_DIR)$(LIBDIR) \
	-sGCC_ROOT_DIRECTORY=$(GCC_ROOT) -sGCC=gcc -sGXX=g++ \
	--user-config=./user-config.jam

COMPONENT_BUILD_ENV += CC="$(CC)" CXX="$(CXX)" LDFLAGS="$(LDFLAGS)"

COMPONENT_PRE_BUILD_ACTION = \
			$(MODULES_ENV); \
			$(MODULE_LOAD) mpich/gcc/$(BITS)/latest

COMPONENT_BUILD_ACTION = \
	    		./bootstrap.sh --prefix=$(USRDIR) --libdir=$(LIBDIR) \
				--with-toolset=gcc --with-icu=$(USRDIR); \
			echo 'using mpi ;' > ./user-config.jam; \
			$(BJAM) release stage

COMPONENT_POST_BUILD_ACTION = \
			$(MODULE_UNLOAD) mpich/gcc/$(BITS)/latest

COMPONENT_PRE_INSTALL_ACTION = \
			$(MODULES_ENV); \
			$(MODULE_LOAD) mpich/gcc/$(BITS)/latest

COMPONENT_INSTALL_ACTION = \
			$(BJAM) install \

COMPONENT_POST_INSTALL_ACTION= \
	$(MKDIR) $(PROTO_DIR)$(DOCDIR); \
	cd $(SOURCE_DIR) && \
	find . -type f \
		\( -name \*.htm\* -o -name \*.css -o -name \*.js \
			-o -name \*.gif -o -name \*.jpg -o -name \*.png -o -name \*.PNG -o -name \*.ico \
			-o -name \*.qbk -o -name \*.pattern \) | \
		$(GTAR) -cf - --files-from=- | $(GTAR) -C $(PROTO_DIR)$(DOCDIR) -xf - ; \
	$(MODULE_UNLOAD) mpich/gcc/$(BITS)/latest
 


$(BUILD_DIR)/%/.built:    $(SOURCE_DIR)/.prep
	$(RM) -r $(@D) ; $(MKDIR) $(@D)
	$(CLONEY) $(SOURCE_DIR) $(@D)
	(cd $(@D);\
		$(COMPONENT_PRE_BUILD_ACTION) ; \
		$(ENV) $(COMPONENT_BUILD_ENV) $(COMPONENT_BUILD_ACTION) ; \
		$(COMPONENT_POST_BUILD_ACTION))
	$(TOUCH) $@

$(BUILD_DIR)/%/.installed:  $(BUILD_DIR)/%/.built
	(cd $(@D); \
		$(COMPONENT_PRE_INSTALL_ACTION) ; \
		$(COMPONENT_INSTALL_ENV) $(COMPONENT_INSTALL_ACTION) ; \
		$(COMPONENT_POST_INSTALL_ACTION))
	$(TOUCH) $@

build: $(BUILD_32_and_64)

install: $(INSTALL_32_and_64)

clean::
	$(RM) -r $(BUILD_DIR) $(PROTO_DIR)
