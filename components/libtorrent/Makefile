#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#

#
# Copyright (c) 2011, Oracle and/or its affiliates. All rights reserved.
#

include ../../make-rules/shared-macros.mk

COMPONENT_NAME=		libtorrent
COMPONENT_VERSION=	0.12.2
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_PROJECT_URL=	http://libtorrent.rakshasa.no/
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	sha1:a53d2c671e9f2dd971d0622d5b3672da91c46ef9
COMPONENT_ARCHIVE_URL=	http://libtorrent.rakshasa.no/downloads/$(COMPONENT_ARCHIVE)

include ../../make-rules/prep.mk
include ../../make-rules/configure.mk
include ../../make-rules/ips.mk

COMPONENT_PRE_CONFIGURE_ACTION = \
	($(CLONEY) $(SOURCE_DIR) $(@D))

COMPONENT_PREP_ACTION = \
        (cd $(@D) ; \
	    aclocal-1.10 -I./scripts -I. ; \
	    autoheader; \
	    libtoolize --automake --copy --force; \
	    automake-1.10; \
	    autoconf )

# Although -norunpath is set for CXXFLAGS, we need to put -norunpath 
# here, otherwise -norunpath doesn't get set when creating the shared 
# libraries (CC -G).
CXX+=   $(studio_NORUNPATH)

# this is needed or we can't compile the rak headers
CC=$(CXX)

CXXFLAGS +=	$(studio_OPT)
CXXFLAGS +=	-i
CXXFLAGS +=	-xspace
CXXFLAGS +=	-mr
CXXFLAGS +=	$(studio_XREGS)

CONFIGURE_OPTIONS  +=	--enable-shared
CONFIGURE_OPTIONS  +=	--disable-debug
CONFIGURE_OPTIONS  +=	--disable-static
CONFIGURE_OPTIONS  +=	--with-ports
CONFIGURE_OPTIONS  +=	--disable-libtool-lock
CONFIGURE_OPTIONS.32 +=	--srcdir=$(BUILD_DIR_32)
CONFIGURE_OPTIONS.64 +=	--srcdir=$(BUILD_DIR_64)
CONFIGURE_OPTIONS  +=	CFLAGS="$(CFLAGS)"
CONFIGURE_OPTIONS  +=	CXXFLAGS="$(CXXFLAGS)"


# common targets
build:		$(BUILD_32_and_64)

install:	$(INSTALL_32_and_64)

test:		$(NO_TESTS)

BUILD_PKG_DEPENDENCIES =	$(BUILD_TOOLS)

include ../../make-rules/depend.mk
