AC_PREREQ(2.59)
AC_INIT([libgrok],[1.0])
AM_INIT_AUTOMAKE([foreign]) 

AC_CONFIG_MACRO_DIR([m4])

AC_PROG_CC
AC_PROG_LIBTOOL

AC_PROG_YACC
AM_PROG_LEX

PKG_PROG_PKG_CONFIG

LT_INIT([dlopen])

AM_CONFIG_HEADER(grok_version.h)

AC_CHECK_PROG(GPERF, gperf, gperf)

if test "$GPERF" = ""; then
 AC_MSG_ERROR([gperf not found])
fi

AC_DEFINE_UNQUOTED(GROK_VERSION, "$VERSION",[Version])

AC_CHECK_HEADERS(event.h)
if test "$ac_cv_header_event_h" != "yes"; then
 AC_MSG_ERROR([event.h missing, perhaps libevent dev library is not installed])
fi

PKG_CHECK_MODULES(TOKYOCABINET, tokyocabinet,,)

AC_CONFIG_FILES([Makefile libgrok.pc])
AC_OUTPUT

