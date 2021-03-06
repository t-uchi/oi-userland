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

COMPONENT_NAME=		ipmitool
COMPONENT_VERSION=	1.8.10
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_PROJECT_URL=	http://ipmitool.sourceforge.net
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
    sha256:13a0e40faf266e0eea6e4cb8136a00ce67ea85d18392e6384be17898d76cbd12
COMPONENT_ARCHIVE_URL=	http://downloads.sourceforge.net/project/ipmitool/ipmitool/$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)

include ../../make-rules/prep.mk
include ../../make-rules/configure.mk
include ../../make-rules/ips.mk

# The version of libtool in the source archive causes the build to fail to
# link in src/plugins/lan.  The bundled vesion works fine.
COMPONENT_PREP_ACTION=(cd $(@D) ; libtoolize -f)

COMPILER=gcc

CONFIGURE_OPTIONS  +=		--prefix=/usr/sfw
CONFIGURE_OPTIONS  +=		--enable-intf-free=no
CONFIGURE_OPTIONS  +=		CFLAGS="$(CFLAGS)"


# common targets
build:		$(BUILD_32_and_64)

install:	$(INSTALL_32_and_64)

# run test_ipmitool && test_ipmievd as root vs self
# on test vs build machine in tmp vs workspace dir
test:		$(TESTS_32_and_64)

BUILD_PKG_DEPENDENCIES =	$(BUILD_TOOLS)

include ../../make-rules/depend.mk
