
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

COMPONENT_NAME=		infiniband-diags
COMPONENT_VERSION=	1.5.13
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	sha256:9d3197414936d072c0bd72b9d4fb92bb31f017ef4aec2fd0efb3f3ef3c85cedd
COMPONENT_ARCHIVE_URL=	http://www.openfabrics.org/downloads/management/$(COMPONENT_ARCHIVE)

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include ../ofed.mk

MAN1MFILES = set_nodedesc.sh.1m

include $(WS_TOP)/make-rules/shared-targets.mk

CFLAGS += -I$(PROTO_DIR)/usr/include/infiniband
LIBS +=	-lsocket -lnsl -lopensm -losmvendor -losmcomp -libumad -libmad -libverbs -ldevinfo

COMPONENT_PREP_ACTION = \
        cp solaris_set_nodedesc.c $(@D)/src

COMPONENT_INSTALL_ENV +=	PERL=$(PERL)

CONFIGURE_ENV +=	PERL=$(PERL)

# it apears that configure is broken
COMPONENT_BUILD_ARGS  +=	LIBS="$(LIBS)"

COMPONENT_PRE_CONFIGURE_ACTION =\
	$(SYMLINK) ../../$(COMPONENT_SRC)/include $(@D)/include

COMPONENT_POST_CONFIGURE_ACTION=\
	$(SYMLINK) ../../../$(COMPONENT_SRC)/scripts/IBswcountlimits.pm $(@D)/scripts

PROTOMAN = $(PROTO_DIR)/$(CONFIGURE_MANDIR)

CLEANUP_FILES =\
	$(PROTO_DIR)/$(CONFIGURE_LIBDIR.32)/libibnetdisc.la\
	$(PROTO_DIR)/$(CONFIGURE_LIBDIR.32)/libibnetdisc.so \
	$(PROTOUSRBINDIR)/vendstat\
	$(PROTOUSRBINDIR)/dump_lfts.sh \
	$(PROTOUSRBINDIR)/dump_mfts.sh\
	$(PROTOUSRBINDIR)/ibidsverify.pl \
	$(PROTOUSRBINDIR)/ibfindnodesusing.pl\
	$(PROTOMAN)/man1m/vendstat.1m \
	$(PROTOMAN)/man1m/dump_lfts.1m\
	$(PROTOMAN)/man1m/dump_mfts.1m \
	$(PROTOMAN)/man1m/ibidsverify.1m\
	$(PROTOMAN)/man1m/ibfindnodesusing.1m \
	$(PROTOUSRINCDIR)/infiniband/ibnetdisc.h\

COMPONENT_POST_INSTALL_ACTION =\
	$(RM) $(CLEANUP_FILES);\
	$(INSTALL) -m 644 manpages/set_nodedesc.sh.1m $(PROTOMAN)/man1m

# common targets
build:		$(BUILD_32)

install:	$(INSTALL_32) $(PROTOMAN1MFILES)

BUILD_PKG_DEPENDENCIES =	$(BUILD_TOOLS)

test:		$(NO_TESTS)

include $(WS_TOP)/make-rules/depend.mk
