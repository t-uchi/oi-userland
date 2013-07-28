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
# Copyright (c) 2011, Oracle and/or its affiliates. All rights reserved.
#
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		qperf
COMPONENT_VERSION=	0.4.9
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	sha256:2300e75edffe95d4dfbe576eb5c2f0d0da3142b5e4a96fcd01b535d50a48f07c
COMPONENT_ARCHIVE_URL=	http://www.openfabrics.org/downloads/qperf/$(COMPONENT_ARCHIVE)

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include ../ofed.mk

LIBS +=         -lsocket -lnsl -lkstat -lrdmacm -libverbs

COMPONENT_INSTALL_ENV +=	INSTALL="$(INSTALL) -m 755"

COMPONENT_PRE_CONFIGURE_ACTION = \
        (mkdir $(@D)/src ; cd $(@D)/src ; ln -s $(SOURCE_DIR)/src/help.txt ; \
         ln -s $(SOURCE_DIR)/src/mkhelp ; ln -s $(SOURCE_DIR)/src/mkman)

# common targets
build:		$(BUILD_32_and_64)

install:	$(INSTALL_32_and_64)

BUILD_PKG_DEPENDENCIES =	$(BUILD_TOOLS)

test:		$(NO_TESTS)

include $(WS_TOP)/make-rules/depend.mk
