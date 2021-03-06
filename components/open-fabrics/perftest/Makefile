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

COMPONENT_NAME=		perftest
COMPONENT_VERSION=	1.3.0
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC)-0.58.g8f82435.tar.gz
COMPONENT_ARCHIVE_HASH=	sha256:26b68938036265507e4ea9a4c56b5ca9686b009628de4b96124c7f7aec4d93e2
COMPONENT_ARCHIVE_URL=	http://www.openfabrics.org/downloads/perftest/$(COMPONENT_ARCHIVE)

$(BUILD_32):	BITS=32
$(BUILD_64):	BITS=64
$(INSTALL_32):	BITS=32
$(INSTALL_64):	BITS=64

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include ../ofed.mk

MAN1FILES =	ib_clock_test.1

include $(WS_TOP)/make-rules/shared-targets.mk

LIBS +=         -lsocket -lnsl -lkstat -lrdmacm -libverbs -libumad -libmad

LDFLAGS +=	-L$(PROTO_DIR)/$(CONFIGURE_LIBDIR.$(BITS))
CFLAGS +=	$(SHARED_INCLUDES)

COMMON_ARGS  +=	CC="$(CC)"
COMMON_ARGS  +=	CFLAGS="$(CFLAGS)"
COMMON_ARGS  +=	LDFLAGS="$(LDFLAGS) $(LIBS)"
COMMON_ARGS  +=	INSTALL=$(INSTALL)
COMMON_ARGS  +=  BINDIR=$(CONFIGURE_BINDIR.$(BITS))
COMPONENT_BUILD_ARGS  +=	$(COMMON_ARGS)
COMPONENT_INSTALL_ARGS  +=	$(COMMON_ARGS)

COMPONENT_PREP_ACTION = $(TOUCH) $(@D)/configure

COMPONENT_PRE_CONFIGURE_ACTION = ($(CLONEY) $(SOURCE_DIR) $(@D))

# common targets
build:		$(BUILD_32_and_64)

install:	$(INSTALL_32_and_64) $(PROTOMAN1FILES)

BUILD_PKG_DEPENDENCIES =	$(BUILD_TOOLS)

test:		$(NO_TESTS)

include $(WS_TOP)/make-rules/depend.mk
