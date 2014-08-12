AC_PREREQ(2.59)
AC_INIT([libgrok],[1.0])
AM_INIT_AUTOMAKE([foreign]) 

AC_CONFIG_MACRO_DIR([m4])

AC_PROG_CC
AC_PROG_LIBTOOL

AC_PROG_YACC
AM_PROG_LEX

LT_INIT([dlopen])

AC_CHECK_PROG(GPERF, gperf, gperf, [ AC_MSG_ERROR([gperf not found]) ])

AC_CONFIG_FILES([Makefile libgrok.pc])
AC_OUTPUT

