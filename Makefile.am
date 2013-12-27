ACLOCAL_AMFLAGS = -I build
SUBDIRS = @TOPLEVEL_SUBDIRS@ tests

CLEANFILES =
MAINTAINERCLEANFILES =

CLEANFILES += tests/regression/server_root/conf/*.t_*.conf \
    tests/regression/server_root/logs/*.log

MAINTAINERCLEANFILES += $(CLEANFILES) \
    aclocal.m4 \
    alp2/Makefile.in \
    apache2/Makefile.in \
    build/config.guess \
    build/config.sub \
    build/depcomp \
    build/libtool.m4 \
    build/ltmain.sh \
    build/lt~obsolete.m4 \
    build/ltoptions.m4 \
    build/ltsugar.m4 \
    build/ltversion.m4 \
    build/missing \
    config.log \
    config.status \
    configure \
    ext/Makefile.in \
    Makefile \
    Makefile.in \
    mlogc/Makefile.in \
    modsecurity_config_auto.h.in~

test: check

test-regression:
	(cd tests && $(MAKE) test-regression)

cppcheck:
	cppcheck . --enable=all --force 2>&1 | sed 's/^/warning: /g' 1>&2;

check-coding-style:
	for i in `(find . -iname "*.c" ; find . -iname "*.h")`; \
	    do echo $$i...; \
	    vera++ -rule L004 -param max-line-length=80 $$i 2>&1 | sed 's/^/warning: /g' 1>&2; \
	    vera++ -rule L001 $$i 2>&1 | sed 's/^/warning: /g' 1>&2; \
	done; 

guess-version:
	major=`cat msc_release.h | grep "#define MODSEC_VERSION_MAJOR" | awk {'print $3'} | sed 's/"//g'`
	minor=`cat msc_release.h | grep "#define MODSEC_VERSION_MINOR" | awk {'print $3'} | sed 's/"//g'`
	maint=`cat msc_release.h | grep "#define MODSEC_VERSION_MAINT" | awk {'print $3'} | sed 's/"//g'`
	commit=``


.PHONY: test
