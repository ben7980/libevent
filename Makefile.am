# Makefile.am for libevent
# Copyright 2000-2007 Niels Provos
# Copyright 2007-2012 Niels Provos and Nick Mathewson
#
# See LICENSE for copying information.

ACLOCAL_AMFLAGS = -I m4

# This is the "Release" of the Libevent ABI.  It takes precedence over
# the VERSION_INFO, so that two versions of Libevent with the same
# "Release" are never binary-compatible.
#
# This number incremented once for the 2.0 release candidate, and
# will increment for each series until we revise our interfaces enough
# that we can seriously expect ABI compatibility between series.
#
RELEASE = -release 2.2

# This is the version info for the libevent binary API.  It has three
# numbers:
#   Current  -- the number of the binary API that we're implementing
#   Revision -- which iteration of the implementation of the binary
#               API are we supplying?
#   Age      -- How many previous binary API versions do we also
#               support?
#
# To increment a VERSION_INFO (current:revision:age):
#    If the ABI didn't change:
#        Return (current:revision+1:age)
#    If the ABI changed, but it's backward-compatible:
#        Return (current+1:0:age+1)
#    If the ABI changed and it isn't backward-compatible:
#        Return (current+1:0:0)
#
# Once an RC is out, DO NOT MAKE ANY ABI-BREAKING CHANGES IN THAT SERIES
# UNLESS YOU REALLY REALLY HAVE TO.
VERSION_INFO = 1:0:0

# History:          RELEASE    VERSION_INFO
#  2.0.1-alpha --     2.0        1:0:0
#  2.0.2-alpha --                2:0:0
#  2.0.3-alpha --                2:0:0  (should have incremented; didn't.)
#  2.0.4-alpha --                3:0:0
#  2.0.5-beta  --                4:0:0
#  2.0.6-rc    --     2.0        2:0:0
#  2.0.7-rc    --     2.0        3:0:1
#  2.0.8-rc    --     2.0        4:0:2
#  2.0.9-rc    --     2.0        5:0:0 (ABI changed slightly)
#  2.0.10-stable--    2.0        5:1:0 (No ABI change)
#  2.0.11-stable--    2.0        6:0:1 (ABI changed, backward-compatible)
#  2.0.12-stable--    2.0        6:1:1 (No ABI change)
#  2.0.13-stable--    2.0        6:2:1 (No ABI change)
#  2.0.14-stable--    2.0        6:3:1 (No ABI change)
#  2.0.15-stable--    2.0        6:3:1 (Forgot to update :( )
#  2.0.16-stable--    2.0        6:4:1 (No ABI change)
#  2.0.17-stable--    2.0        6:5:1 (No ABI change)
#  2.0.18-stable--    2.0        6:6:1 (No ABI change)
#  2.0.19-stable--    2.0        6:7:1 (No ABI change)
#  2.0.20-stable--    2.0        6:8:1 (No ABI change)
#  2.0.21-stable--    2.0        6:9:1 (No ABI change)
#
# For Libevent 2.1:
#  2.1.1-alpha --     2.1        1:0:0
#  2.1.2-alpha --     2.1        1:0:0 (should have been 2:0:1)
#  2.1.3-alpha --     2.1        3:0:0 (ABI changed slightly)
#  2.1.4-alpha --     2.1        4:0:0 (ABI changed slightly)
#  2.1.5-beta  --     2.1        5:0:0 (ABI changed slightly)
#  2.1.6-beta  --     2.1        6:0:0 (ABI changed slightly)
#  2.1.7-beta  --     2.1        6:1:0 (ABI changed slightly)
#  2.1.8-stable--     2.1        6:2:0 (ABI changed slightly)
#
# For Libevent 2.2:
#  2.2.1-alpha --     2.2        1:0:0

# ABI version history for this package effectively restarts every time
# we change RELEASE.  Version 1.4.x had RELEASE of 1.4.
#
# Ideally, we would not be using RELEASE at all; instead we could just
# use the VERSION_INFO field to label our backward-incompatible ABI
# changes, and those would be few and far between.  Unfortunately,
# Libevent still exposes far too many volatile structures in its
# headers, so we pretty much have to assume that most development
# series will break ABI compatibility.  For now, it's simplest just to
# keep incrementing the RELEASE between series and resetting VERSION_INFO.
#
# Eventually, when we get to the point where the structures in the
# headers are all non-changing (or not there at all!), we can shift to
# a more normal worldview where backward-incompatible ABI changes are
# nice and rare.  For the next couple of years, though, 'struct event'
# is user-visible, and so we can pretty much guarantee that release
# series won't be binary-compatible.

if INSTALL_LIBEVENT
dist_bin_SCRIPTS = event_rpcgen.py
endif

pkgconfigdir=$(libdir)/pkgconfig
LIBEVENT_PKGCONFIG=libevent.pc libevent_core.pc libevent_extra.pc

# These sources are conditionally added by configure.ac or conditionally
# included from other files.
PLATFORM_DEPENDENT_SRC = \
	arc4random.c \
	bufferevent_ssl.c \
	epoll_sub.c \
	PrivacyInfo.xcprivacy \
	test/regress_ssl.c

CMAKE_FILES = \
	cmake/AddCompilerFlags.cmake \
	cmake/AddLinkerFlags.cmake \
	cmake/AddEventLibrary.cmake \
	cmake/CheckConstExists.cmake \
	cmake/CheckFileOffsetBits.c \
	cmake/CheckFileOffsetBits.cmake \
	cmake/CheckFunctionKeywords.cmake \
	cmake/CheckPrototypeDefinition.c.in \
	cmake/CheckPrototypeDefinition.cmake \
	cmake/CheckWorkingKqueue.cmake \
	cmake/CodeCoverage.cmake \
	cmake/COPYING-CMAKE-SCRIPTS \
	cmake/Copyright.txt \
	cmake/FindMbedTLS.cmake \
	cmake/LibeventConfig.cmake.in \
	cmake/LibeventConfigVersion.cmake.in \
	cmake/Macros.cmake \
	cmake/Uninstall.cmake.in \
	cmake/UseDoxygen.cmake \
	cmake/VersionViaGit.cmake \
	event-config.h.cmake \
	evconfig-private.h.cmake \
	CMakeLists.txt

DOCUMENTATION_FILES = \
	Documentation/Building.md

EXTRA_DIST = \
	ChangeLog-1.4 \
	ChangeLog-2.0 \
	ChangeLog-2.1 \
	ChangeLog \
	Doxyfile \
	LICENSE \
	autogen.sh \
	event_rpcgen.py \
	libevent.pc.in \
	make-event-config.sed \
	whatsnew-2.0.txt \
	whatsnew-2.1.txt \
	README.md \
	$(CMAKE_FILES) \
	$(DOCUMENTATION_FILES) \
	$(PLATFORM_DEPENDENT_SRC)

LIBEVENT_LIBS_LA = libevent.la libevent_core.la libevent_extra.la
if PTHREADS
LIBEVENT_LIBS_LA += libevent_pthreads.la
LIBEVENT_PKGCONFIG += libevent_pthreads.pc
endif
if OPENSSL
LIBEVENT_LIBS_LA += libevent_openssl.la
LIBEVENT_PKGCONFIG += libevent_openssl.pc
endif
if MBEDTLS
LIBEVENT_LIBS_LA += libevent_mbedtls.la
LIBEVENT_PKGCONFIG += libevent_mbedtls.pc
endif

if INSTALL_LIBEVENT
lib_LTLIBRARIES = $(LIBEVENT_LIBS_LA)
pkgconfig_DATA = $(LIBEVENT_PKGCONFIG)
else
noinst_LTLIBRARIES =  $(LIBEVENT_LIBS_LA)
endif

EXTRA_SOURCE=
noinst_HEADERS=
noinst_PROGRAMS=
EXTRA_PROGRAMS=
CLEANFILES=
DISTCLEANFILES=
BUILT_SOURCES =
include include/include.am
include sample/include.am
include test/include.am

if BUILD_WIN32

SYS_CORE_LIBS = -liphlpapi
SYS_LIBS = -lws2_32 -lshell32 -ladvapi32 -lbcrypt
SYS_SRC = win32select.c buffer_iocp.c event_iocp.c \
	bufferevent_async.c
SYS_INCLUDES = -IWIN32-Code

if THREADS
SYS_SRC += evthread_win32.c
endif

else

SYS_CORE_LIBS =
SYS_LIBS =
SYS_SRC =
SYS_INCLUDES =

endif

if STRLCPY_IMPL
SYS_SRC += strlcpy.c
endif
if SELECT_BACKEND
SYS_SRC += select.c
endif
if POLL_BACKEND
SYS_SRC += poll.c
endif
if DEVPOLL_BACKEND
SYS_SRC += devpoll.c
endif
if KQUEUE_BACKEND
SYS_SRC += kqueue.c
endif
if EPOLL_BACKEND
SYS_SRC += epoll.c
endif
if EVPORT_BACKEND
SYS_SRC += evport.c
endif
if WEPOLL_BACKEND
SYS_SRC += epoll.c
SYS_SRC += wepoll.c
endif
if SIGNAL_SUPPORT
SYS_SRC += signal.c
endif
if SIGNALFD_SUPPORT
SYS_SRC += signalfd.c
endif

BUILT_SOURCES += include/event2/event-config.h

include/event2/event-config.h: config.h make-event-config.sed
	$(AM_V_GEN)test -d include/event2 || $(MKDIR_P) include/event2
	$(AM_V_at)$(SED) -f $(srcdir)/make-event-config.sed < config.h > $@T
	$(AM_V_at)mv -f $@T $@

CORE_SRC =					\
	buffer.c				\
	bufferevent.c				\
	bufferevent_filter.c			\
	bufferevent_pair.c			\
	bufferevent_ratelim.c			\
	bufferevent_sock.c			\
	event.c					\
	evmap.c					\
	evthread.c				\
	evutil.c				\
	evutil_rand.c				\
	evutil_time.c				\
	watch.c					\
	listener.c				\
	log.c					\
	$(SYS_SRC)

EXTRAS_SRC =					\
	evdns.c					\
	event_tagging.c				\
	evrpc.c					\
	sha1.c					\
	ws.c					\
	http.c

if BUILD_WITH_NO_UNDEFINED
NO_UNDEFINED = -no-undefined
MAYBE_CORE = libevent_core.la
else
NO_UNDEFINED =
MAYBE_CORE =
endif

AM_CFLAGS = $(LIBEVENT_CFLAGS)
AM_CPPFLAGS = -I$(srcdir)/compat -I./include -I$(srcdir)/include $(SYS_INCLUDES) $(LIBEVENT_CPPFLAGS)
AM_LDFLAGS = $(LIBEVENT_LDFLAGS)

GENERIC_LDFLAGS = -version-info $(VERSION_INFO) $(RELEASE) $(NO_UNDEFINED) $(AM_LDFLAGS)

libevent_la_SOURCES = $(CORE_SRC) $(EXTRAS_SRC)
libevent_la_LIBADD = @LTLIBOBJS@ $(SYS_LIBS) $(SYS_CORE_LIBS)
libevent_la_LDFLAGS = $(GENERIC_LDFLAGS)

libevent_core_la_SOURCES = $(CORE_SRC)
libevent_core_la_LIBADD = @LTLIBOBJS@ $(SYS_LIBS) $(SYS_CORE_LIBS)
libevent_core_la_LDFLAGS = $(GENERIC_LDFLAGS)

if PTHREADS
libevent_pthreads_la_SOURCES = evthread_pthread.c
libevent_pthreads_la_LIBADD = $(MAYBE_CORE)
libevent_pthreads_la_LDFLAGS = $(GENERIC_LDFLAGS)
endif

libevent_extra_la_SOURCES = $(EXTRAS_SRC)
libevent_extra_la_LIBADD = $(MAYBE_CORE) $(SYS_LIBS)
libevent_extra_la_LDFLAGS = $(GENERIC_LDFLAGS)

if OPENSSL
libevent_openssl_la_SOURCES = bufferevent_openssl.c bufferevent_ssl.c
libevent_openssl_la_LIBADD = $(MAYBE_CORE) $(OPENSSL_LIBS)
libevent_openssl_la_LDFLAGS = $(GENERIC_LDFLAGS)
libevent_openssl_la_CPPFLAGS = $(AM_CPPFLAGS) $(OPENSSL_INCS)
endif

if MBEDTLS
libevent_mbedtls_la_SOURCES = bufferevent_mbedtls.c bufferevent_ssl.c
libevent_mbedtls_la_LIBADD = $(MAYBE_CORE) $(MBEDTLS_LIBS)
libevent_mbedtls_la_LDFLAGS = $(GENERIC_LDFLAGS)
libevent_mbedtls_la_CPPFLAGS = $(AM_CPPFLAGS) $(MBEDTLS_INCS)
endif

noinst_HEADERS +=				\
	WIN32-Code/getopt.h			\
	WIN32-Code/getopt.c			\
	WIN32-Code/getopt_long.c	\
	WIN32-Code/tree.h			\
	bufferevent-internal.h		\
	changelist-internal.h		\
	compat/sys/queue.h			\
	compat/sys/tree.h			\
	defer-internal.h			\
	epolltable-internal.h		\
	evbuffer-internal.h			\
	event-internal.h			\
	evmap-internal.h			\
	evrpc-internal.h			\
	evsignal-internal.h			\
	evthread-internal.h			\
	evdns-internal.h			\
	ht-internal.h				\
	http-internal.h				\
	iocp-internal.h				\
	ipv6-internal.h				\
	kqueue-internal.h			\
	log-internal.h				\
	minheap-internal.h			\
	mm-internal.h				\
	ratelim-internal.h			\
	ratelim-internal.h			\
	strlcpy-internal.h			\
	time-internal.h				\
	util-internal.h				\
	openssl-compat.h			\
	mbedtls-compat.h			\
	sha1.h						\
	ssl-compat.h			    \
	wepoll.h

EVENT1_HDRS = \
	include/evdns.h \
	include/event.h \
	include/evhttp.h \
	include/evrpc.h \
	include/evutil.h

if INSTALL_LIBEVENT
include_HEADERS = $(EVENT1_HDRS)
else
noinst_HEADERS += $(EVENT1_HDRS)
endif

verify: check

include doxygen.am

DISTCLEANFILES += *~ libevent.pc libevent_core.pc libevent_extra.pc ./include/event2/event-config.h

