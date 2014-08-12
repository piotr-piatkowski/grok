lib_LTLIBRARIES = libgrok.la
libgrok_la_SOURCES = grok.c \
                grok_capture.c \
		grok_capture_xdr.c \
	 	grok_config.c \
		grok_discover.c \
		grok_input.c \
		grok_logging.c \
		grok_match.c \
		grok_matchconf.c \
		grok_matchconf_macro.c \
		grok_pattern.c \
		grok_program.c \
		grokre.c \
		filters.c \
		libc_helper.c \
		predicates.c \
		stringhelper.c \
		conf.tab.c \
		conf.yy.c

libgrok_la_LIBADD = -ltokyocabinet -lpcre -levent -ldl

bin_PROGRAMS = grok discover
grok_SOURCES = main.c
grok_LDADD = -lgrok

discover_SOURCES = discover_main.c
discover_LDADD = -lgrok

include_HEADERS = filters.h \
		  grok.h \
	          grok_capture_xdr.h \
		  grok_logging.h \
                  grok_capture.h \
 		  grok_config.h  \
 		  grok_discover.h \
		  grok_input.h \
		  grok_match.h \
		  grok_matchconf.h \
		  grok_matchconf_macro.h \
		  grok_pattern.h \
		  grok_program.h \
		  grok_version.h \
		  libc_helper.h \
  		  predicates.h \
		  stringhelper.h

extra_DIST = libgrok.pc
pkg_configdir = ${libdir}/pkgconfig
pkg_config_DATA = libgrok.pc

BUILT_SOURCES = grok_capture_xdr.c grok_capture_xdr.h grok_matchconf_macro.c filters.c conf.tab.c conf.tab.h conf.yy.c grok_logging.h

EXTRA_DIST = grok_capture.x conf.y conf.lex conf.yy.c conf.tab.h

conf.tab.c conf.tab.h: conf.y
	bison -d $<

conf.yy.c: conf.lex conf.tab.h
	@if $(LEX) --version | grep '^flex version' ; then \
                if [ "$(FORCE_FLEX)" -eq 1 ] ; then \
                        echo "Bad version of flex detected, but FORCE_FLEX is set, trying anyway."; \
                        exit 0; \
                fi; \
                echo "Fatal - cannot build"; \
                echo "You need GNU flex. You seem to have BSD flex?"; \
                strings `which flex` | grep Regents; \
                echo "If you want to try your flex, anyway, set FORCE_FLEX=1"; \
                exit 1; \
        fi
	$(LEX) -o $@ $<

grok_capture_xdr.c: grok_capture.x
	[ -f $@ ] && rm $@ || true
	rpcgen -c $< -o $@
grok_capture_xdr.h: grok_capture.x
	[ -f $@ ] && rm $@ || true
	rpcgen -h $< -o $@

%.c: %.gperf
	@if $(GPERF) --version | head -1 | egrep -v '3\.[0-9]+\.[0-9]+' ; then \
                echo "We require gperf version >= 3.0.3" ; \
                exit 1; \
        fi
	$(GPERF) $< > $@
