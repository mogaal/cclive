#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.68])

m4_include([m4/version.m4])

AC_INIT([cclive], [_CCLIVE_VERSION],
  [http://sourceforge.net/apps/trac/cclive], [],
  [http://cclive.sourceforge.net/])

AC_CONFIG_SRCDIR([src/cc/application.cpp])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_AUX_DIR([config.aux])
AC_CONFIG_MACRO_DIR([m4])

AC_CANONICAL_SYSTEM
AC_GNU_SOURCE

AC_DEFINE_UNQUOTED([CANONICAL_TARGET], "$target", [...])
AC_DEFINE_UNQUOTED([CANONICAL_HOST], "$host", [...])

AM_INIT_AUTOMAKE([-Wall -Werror foreign dist-bzip2 dist-xz])
AM_SILENT_RULES([yes])

LT_INIT()
LT_PREREQ([2.2])

# Checks for programs.
AC_PROG_CXX
AC_PROG_CC
AC_PROG_CPP

# Checks for libraries.

PKG_CHECK_MODULES([libquvi], [libquvi >= 0.4.0],
  [AC_DEFINE([HAVE_LIBQUVI_0_4_0], [1], [We have libquvi 0.4.0+])],
  [PKG_CHECK_MODULES([libquvi], [libquvi >= 0.2.16.1])])
PKG_CHECK_MODULES([libcurl], [libcurl >= 7.18.0])
PKG_CHECK_MODULES([libpcre], [libpcre >= 8.02])
PKG_CHECK_MODULES([libpcrecpp], [libpcrecpp >= 8.02])

BOOST_REQUIRE([1.42.0])
# Boost: Header-only libs
BOOST_FOREACH
BOOST_FORMAT
# Boost: Libs requiring linking
BOOST_DATE_TIME
BOOST_PROGRAM_OPTIONS
BOOST_IOSTREAMS
BOOST_FILESYSTEM
BOOST_SYSTEM

# Checks for header files.
AC_CHECK_HEADERS([sys/ioctl.h unistd.h sys/types.h sys/stat.h signal.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_STDBOOL
AC_TYPE_SIZE_T
AC_TYPE_PID_T

# Checks for library functions.
AC_CHECK_FUNCS([strerror strstr getpid signal])
AC_FUNC_ERROR_AT_LINE
AC_FUNC_STRERROR_R
AC_FUNC_FORK

# Version.
VN=`$srcdir/gen-ver.sh $srcdir`
AC_DEFINE_UNQUOTED([VN],["$VN"], [We have version number from gen-ver.sh])

# --with-manual
AC_ARG_WITH([manual],
  [AS_HELP_STRING([--with-manual],
    [Install manual page(s) @<:@default=yes@:>@])],
  [],
  [with_manual=yes])
AM_CONDITIONAL([WITH_MANUAL], [test x"$with_manual" != "xno"])

# --enable-ccl
AC_ARG_ENABLE([ccl],
  [AS_HELP_STRING([--enable-ccl],
    [Make a symbolic link from 'cclive' to 'ccl' @<:@default=no@:>@])],
  [],
  [enable_ccl=no])
AM_CONDITIONAL([ENABLE_CCL], [test x"$enable_ccl" != "xno"])

AC_CONFIG_FILES([
  Makefile
  doc/Makefile
  doc/man1/Makefile
  src/Makefile
])

AC_OUTPUT

AC_MSG_NOTICE([
 cclive version: ${VERSION} (${VN})
 host setup:     ${host}
 prefix:         ${prefix}
 install manual: ${with_manual}])

# vim: set ts=2 sw=2 tw=72 expandtab: