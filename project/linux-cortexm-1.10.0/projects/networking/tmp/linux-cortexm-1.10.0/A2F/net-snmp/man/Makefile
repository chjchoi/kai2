#
# Minimum environment and virtual path setup
#
SHELL		= /bin/sh
srcdir		= .
top_srcdir	= ..
VERSION		= 5.6.1


#
# Paths
#
prefix		= /work/psl/SF/release/cm-1.10.0/linux-cortexm-1.10.0/A2F/root/usr
exec_prefix	= ${prefix}
bindir		= ${exec_prefix}/bin
sbindir		= ${exec_prefix}/sbin
libdir		= ${exec_prefix}/lib
datarootdir	= ${prefix}/share
datadir		= ${datarootdir}
includedir	= ${prefix}/include/net-snmp
ucdincludedir	= ${prefix}/include/ucd-snmp
mandir		= ${datarootdir}/man
man1dir		= $(mandir)/man1
man3dir		= $(mandir)/man3
man5dir		= $(mandir)/man5
man8dir		= $(mandir)/man8
snmplibdir	= $(datadir)/snmp
mibdir		= $(snmplibdir)/mibs
persistentdir	= /var/lib/snmp
DESTDIR         = 
INSTALL_PREFIX  = $(DESTDIR)

#
# Programs
#
INSTALL		= $(LIBTOOL) --mode=install /usr/bin/install -c
UNINSTALL	= $(LIBTOOL) --mode=uninstall rm -f
LIBTOOLCLEAN	= $(LIBTOOL) --mode=clean rm -f
INSTALL_DATA    = ${INSTALL} -m 644
SED		= /bin/sed
LN_S		= ln -s
AUTOCONF	= :
AUTOHEADER	= :
PERL            = /usr/bin/perl
PYTHON          = /usr/bin/python
FIND            = find

#
# Compiler arguments
#
CFLAGS		= -fno-strict-aliasing -Os -mcpu=cortex-m3 -mthumb -I/work/psl/SF/release/cm-1.10.0/linux-cortexm-1.10.0/A2F/root/usr/include -Uuclinux -Duclinux=uclinux -Wall -Wstrict-prototypes -Wwrite-strings -Wcast-qual
EXTRACPPFLAGS	= -x c
LDFLAGS		= -mcpu=cortex-m3 -mthumb -L/work/psl/SF/release/cm-1.10.0/linux-cortexm-1.10.0/A2F/root/usr/lib 
LIBTOOL		= $(SHELL) $(top_builddir)/libtool 
EXEEXT		= 

# Misc Compiling Stuff
CC	        = arm-uclinuxeabi-gcc
LINKCC	        = arm-uclinuxeabi-gcc

# use libtool versioning the way they recommend.
# The (slightly clarified) rules:
#
# - If any interfaces/structures have been removed or changed since the
#   last update, increment current (+5), and set age and revision to 0. Stop.
#
# - If any interfaces have been added since the last public release, then
#   increment current and age, and set revision to 0. Stop.
# 
# - If the source code has changed at all since the last update,
#   then increment revision (c:r:a becomes c:r+1:a). 
#
# Note: maintenance releases (eg 5.2.x) should never have changes
#       that would require a current to be incremented.
#
# policy: we increment major releases of LIBCURRENT by 5 starting at
# 5.3 was at 10, 5.4 is at 15, ...  This leaves some room for needed
# changes for past releases if absolutely necessary.
#
LIBCURRENT  = 25
LIBAGE      = 0
LIBREVISION = 1

LIB_LD_CMD      = $(LIBTOOL) --mode=link $(LINKCC) $(CFLAGS) -rpath $(libdir) -version-info $(LIBCURRENT):$(LIBREVISION):$(LIBAGE) -o
LIB_EXTENSION   = la
LIB_VERSION     =
LIB_LDCONFIG_CMD = $(LIBTOOL) --mode=finish $(libdir)
LINK		= $(LIBTOOL) --mode=link $(LINKCC)
# RANLIB 	= ranlib
RANLIB		= :

# libtool definitions
.SUFFIXES: .c .o .lo .rc
.c.lo:
	$(LIBTOOL) --mode=compile $(CC) $(CPPFLAGS) $(CFLAGS) -c -o $@ $<
.rc.lo:
	$(LIBTOOL) --mode=compile --tag=CC windres -o $@ -i $<

# include paths
#
SRC_TOP_INCLUDES            = -I$(top_srcdir)/include
SRC_SNMPLIB_INCLUDES        = -I$(top_srcdir)/snmplib
SRC_AGENT_INCLUDES          = -I$(top_srcdir)/agent
SRC_HELPER_INCLUDES         = -I$(top_srcdir)/agent/helpers
SRC_MIBGROUP_INCLUDES       = -I$(top_srcdir)/agent/mibgroup

BLD_TOP_INCLUDES            = -I$(top_builddir)/include $(SRC_TOP_INCLUDES)
BLD_SNMPLIB_INCLUDES        = -I$(top_builddir)/snmplib $(SRC_SNMPLIB_INCLUDES)
BLD_AGENT_INCLUDES          = -I$(top_builddir)/agent $(SRC_AGENT_INCLUDES)
BLD_HELPER_INCLUDES         = -I$(top_builddir)/agent/helpers $(SRC_HELPER_INCLUDES)
BLD_MIBGROUP_INCLUDES       = -I$(top_builddir)/agent/mibgroup $(SRC_MIBGROUP_INCLUDES)

TOP_INCLUDES            = $(SRC_TOP_INCLUDES)
SNMPLIB_INCLUDES        = $(SRC_SNMPLIB_INCLUDES)
AGENT_INCLUDES          = $(SRC_AGENT_INCLUDES)
HELPER_INCLUDES         = $(SRC_HELPER_INCLUDES)
MIBGROUP_INCLUDES       = $(SRC_MIBGROUP_INCLUDES)

#
# Makefile for the man page directory
#
top_builddir=..


#
# install stuff
#

OTHERINSTALL=maninstall
OTHERUNINSTALL=manuninstall
#
# local stuff
#

MAN1  = snmpinform.1 snmp-bridge-mib.1

#AGENTXTRAP = agentxtrap.1
AGENTXTRAP =

MAN1G = $(AGENTXTRAP) snmpbulkget.1 snmpcmd.1 snmpget.1 snmpset.1 snmpwalk.1 \
	snmpbulkwalk.1 snmpgetnext.1 snmptest.1 snmptranslate.1 snmptrap.1 \
	snmpusm.1 snmpvacm.1 snmptable.1 snmpstatus.1 snmpconf.1 mib2c.1 \
	snmpnetstat.1 snmpdelta.1 snmpdf.1 encode_keychange.1 fixproc.1 \
	net-snmp-config.1 mib2c-update.1 tkmib.1 traptoemail.1 \
	net-snmp-create-v3-user.1

MAN3  = 
MAN3_API = netsnmp_mib_api.3 netsnmp_config_api.3 snmp_alarm.3 \
	netsnmp_session_api.3 netsnmp_sess_api.3 netsnmp_trap_api.3 netsnmp_varbind_api.3 netsnmp_pdu_api.3 
MAN3G = default_store.3 netsnmp_agent_api.3 $(MAN3_API)
MAN5G = snmpd.conf.5 snmptrapd.conf.5 snmp.conf.5 snmp_config.5 variables.5 \
        mib2c.conf.5 snmpd.examples.5 snmpd.internal.5
MAN8G = snmptrapd.8 snmpd.8

MIB_ALIASES     = add_mibdir.3 add_module_replacement.3		\
	fprint_description.3 fprint_objid.3 get_module_node.3	\
	netsnmp_init_mib.3 netsnmp_read_module.3		\
	print_description.3 print_mib.3 print_objid.3		\
	read_all_mibs.3 read_mib.3 read_objid.3			\
	shutdown_mib.3 snmp_parse_oid.3 snmp_set_mib_errors.3	\
	snmp_set_mib_warnings.3 snmp_set_save_descriptions.3	\
	snprint_description.3 snprint_objid.3
CONFIG_ALIASES  = config_perror.3 config_pwarn.3			    \
	read_config_print_usage.3 read_configs.3 read_premib_configs.3	    \
	register_app_config_handler.3 register_app_prenetsnmp_mib_handler.3 \
	register_config_handler.3 register_const_config_handler.3	    \
	register_mib_handlers.3 register_prenetsnmp_mib_handler.3	    \
	unregister_all_config_handlers.3			 	    \
	unregister_app_config_handler.3 unregister_config_handler.3
ALARM_ALIASES   = snmp_alarm_register.3 snmp_alarm_register_hr.3 snmp_alarm_unregister.3
SESSION_ALIASES = snmp_api_errstring.3 snmp_close.3 snmp_error.3    \
	snmp_open.3 snmp_perror.3 snmp_read.3 snmp_select_info.3    \
	snmp_send.3 snmp_sess_perror.3 snmp_timeout.3
SSESS_ALIASES   = snmp_sess_async_send.3 snmp_sess_close.3 snmp_sess_error.3 \
	snmp_sess_init.3 snmp_sess_open.3 snmp_sess_read.3		     \
	snmp_sess_select_info.3 snmp_sess_send.3			     \
	snmp_sess_session.3 snmp_sess_timeout.3
TRAP_ALIASES    = send_easy_trap.3 send_trap_vars.3 send_v2trap.3 
VARBIND_ALIASES = fprint_value.3 fprint_variable.3	\
	print_value.3 print_variable.3			\
	snmp_add_null_var.3 snmp_clone_varbind.3	\
	snmp_free_var.3 snmp_free_varbind.3		\
	snmp_pdu_add_variable.3				\
	snmp_set_var_objid.3 snmp_set_var_typed_integer.3 \
	snmp_set_var_typed_value.3 snmp_set_var_value.3   \
	snmp_varlist_add_variable.3 snprint_value.3 snprint_variable.3
PDU_ALIASES     = snmp_clone_pdu.3 snmp_fix_pdu.3 snmp_free_pdu.3 snmp_pdu_create.3



MANALIASES=$(MIB_ALIASES) $(CONFIG_ALIASES) $(ALARM_ALIASES) $(SESSION_ALIASES) \
	$(SSESS_ALIASES) $(TRAP_ALIASES) $(VARBIND_ALIASES) $(PDU_ALIASES)
MANALL = $(MAN1) $(MAN1G) $(MAN3) $(MAN3G) $(MAN5G) $(MAN8G) $(MANALIASES)

TARGETS = $(MAN5G) $(MAN1G) $(MAN3G) $(MAN8G)
OTHERCLEANTARGETS=$(TARGETS) default_store.3.h $(MANALIASES) manaliases

all: $(TARGETS) standardall manaliases

manaliases: Makefile
	touch manaliases
	@for i in $(MAN3_API) ; do				  \
            for j in `sed -n '/^.SH NAME/,/^.SH SYNOPSIS/p' $$i  | sed -e 's/.- .*//' | sed 's/,.*//'  | /bin/grep -E -v '^.SH ' `; do \
		echo "making man page alias $$j -> $$i APIs" ;    \
		echo ".so man3/$$i" > $$j.3 ; 		  \
	    done                                                  \
	done

agentxtrap.1: $(srcdir)/agentxtrap.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/agentxtrap.1.def > agentxtrap.1

snmpbulkget.1: $(srcdir)/snmpbulkget.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpbulkget.1.def > snmpbulkget.1

snmpbulkwalk.1: $(srcdir)/snmpbulkwalk.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpbulkwalk.1.def > snmpbulkwalk.1

snmpcmd.1: $(srcdir)/snmpcmd.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpcmd.1.def > snmpcmd.1

snmpconf.1: $(srcdir)/snmpconf.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpconf.1.def > snmpconf.1

snmpd.8: $(srcdir)/snmpd.8.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpd.8.def > snmpd.8

snmpdelta.1: $(srcdir)/snmpdelta.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpdelta.1.def > snmpdelta.1

snmpdf.1: $(srcdir)/snmpdf.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpdf.1.def > snmpdf.1

snmpget.1: $(srcdir)/snmpget.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpget.1.def > snmpget.1

snmpgetnext.1: $(srcdir)/snmpgetnext.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpgetnext.1.def > snmpgetnext.1

snmpnetstat.1: $(srcdir)/snmpnetstat.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpnetstat.1.def > snmpnetstat.1

snmpset.1: $(srcdir)/snmpset.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpset.1.def > snmpset.1

snmpstatus.1: $(srcdir)/snmpstatus.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpstatus.1.def > snmpstatus.1

snmptable.1: $(srcdir)/snmptable.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmptable.1.def > snmptable.1

snmptest.1: $(srcdir)/snmptest.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmptest.1.def > snmptest.1

snmptranslate.1: $(srcdir)/snmptranslate.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmptranslate.1.def > snmptranslate.1

snmptrap.1: $(srcdir)/snmptrap.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmptrap.1.def > snmptrap.1

snmpusm.1: $(srcdir)/snmpusm.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpusm.1.def > snmpusm.1

snmpvacm.1: $(srcdir)/snmpvacm.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpvacm.1.def > snmpvacm.1

mib2c.1: $(srcdir)/mib2c.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/mib2c.1.def > mib2c.1

mib2c-update.1: $(srcdir)/mib2c-update.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/mib2c-update.1.def > mib2c-update.1

snmpwalk.1: $(srcdir)/snmpwalk.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpwalk.1.def > snmpwalk.1

encode_keychange.1: $(srcdir)/encode_keychange.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/encode_keychange.1.def > encode_keychange.1

fixproc.1: $(srcdir)/fixproc.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/fixproc.1.def > fixproc.1

net-snmp-config.1: $(srcdir)/net-snmp-config.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/net-snmp-config.1.def > net-snmp-config.1

net-snmp-create-v3-user.1: $(srcdir)/net-snmp-create-v3-user.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/net-snmp-create-v3-user.1.def > net-snmp-create-v3-user.1

tkmib.1: $(srcdir)/tkmib.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/tkmib.1.def > $@

traptoemail.1: $(srcdir)/traptoemail.1.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/traptoemail.1.def > $@

netsnmp_varbind_api.3: $(srcdir)/netsnmp_varbind_api.3.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/netsnmp_varbind_api.3.def > $@

netsnmp_pdu_api.3: $(srcdir)/netsnmp_pdu_api.3.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/netsnmp_pdu_api.3.def > $@

netsnmp_session_api.3: $(srcdir)/netsnmp_session_api.3.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/netsnmp_session_api.3.def > $@

netsnmp_mib_api.3: $(srcdir)/netsnmp_mib_api.3.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/netsnmp_mib_api.3.def > $@

netsnmp_config_api.3: $(srcdir)/netsnmp_config_api.3.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/netsnmp_config_api.3.def > $@

snmp_alarm.3: $(srcdir)/snmp_alarm.3.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmp_alarm.3.def > $@

netsnmp_sess_api.3: $(srcdir)/netsnmp_sess_api.3.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/netsnmp_sess_api.3.def > $@

netsnmp_agent_api.3: $(srcdir)/netsnmp_agent_api.3.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/netsnmp_agent_api.3.def > $@

netsnmp_trap_api.3: $(srcdir)/netsnmp_trap_api.3.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/netsnmp_trap_api.3.def > $@

snmp.conf.5: $(srcdir)/snmp.conf.5.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmp.conf.5.def > $@

snmp_config.5: $(srcdir)/snmp_config.5.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmp_config.5.def > $@

snmpd.conf.5: $(srcdir)/snmpd.conf.5.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpd.conf.5.def > $@

snmpd.examples.5: $(srcdir)/snmpd.examples.5.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpd.examples.5.def > $@

snmpd.internal.5: $(srcdir)/snmpd.internal.5.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmpd.internal.5.def > $@

snmptrapd.conf.5: $(srcdir)/snmptrapd.conf.5.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmptrapd.conf.5.def > $@

variables.5: $(srcdir)/variables.5.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/variables.5.def > $@

snmptrapd.8: $(srcdir)/snmptrapd.8.def ../sedscript
	$(SED) -f ../sedscript < $(srcdir)/snmptrapd.8.def > $@

default_store.3.h: $(srcdir)/../include/net-snmp/library/default_store.h
	awk '{ if ($$0 == "     * begin storage definitions ") { p = 1 } else if ($$0 == "     * end storage definitions ") { p = 0 } else if (p) { print $$0}}' < $(srcdir)/../include/net-snmp/library/default_store.h > default_store.3.h

default_store.3: $(srcdir)/default_store.3.top default_store.3.h $(srcdir)/default_store.3.bot
	$(SED) -f ../sedscript < $(srcdir)/default_store.3.top > default_store.3
	cat default_store.3.h $(srcdir)/default_store.3.bot >> default_store.3

mib2c.conf.5: $(top_srcdir)/local/mib2c mib2c.conf.5.in $(srcdir)/mib2c.extract.pl
	@if test "x$(PERL)" != "x" ; then \
		$(PERL) $(srcdir)/mib2c.extract.pl $(top_srcdir)/local/mib2c $(srcdir)/mib2c.conf.5.in > mib2c.conf.5; \
	else \
	  touch mib2c.conf.5 ; \
	fi

maninstall:  maninstalldirs $(MAN1) $(MAN1G) $(MAN3) $(MAN5G) $(MAN8) $(MANALIASES)
	@for i in $(MAN1) ; do $(INSTALL_DATA) $(srcdir)/$$i $(INSTALL_PREFIX)$(man1dir) ; echo "install:  installed $$i in $(INSTALL_PREFIX)$(man1dir)" ; done
	@$(INSTALL_DATA) $(MAN1G) $(INSTALL_PREFIX)$(man1dir)
	@for i in $(MAN1G) ; do echo "install:  installed $$i in $(INSTALL_PREFIX)$(man1dir)" ; done
	@for i in $(MAN3) ; do $(INSTALL_DATA) $(srcdir)/$$i $(INSTALL_PREFIX)$(man3dir) ; echo "install:  installed $$i in $(INSTALL_PREFIX)$(man3dir)" ; done
	@$(INSTALL_DATA) $(MAN3G) $(INSTALL_PREFIX)$(man3dir)
	@for i in $(MAN3G) ; do echo "install:  installed $$i in $(INSTALL_PREFIX)$(man3dir)" ; done
	@$(INSTALL_DATA) $(MANALIASES) $(INSTALL_PREFIX)$(man3dir)
	@for i in $(MANALIASES) ; do echo "install:  installed $$i in $(INSTALL_PREFIX)$(man3dir)" ; done
	-@$(INSTALL_DATA) $(MAN5G) $(INSTALL_PREFIX)$(man5dir)
	@for i in $(MAN5G) ; do echo "install:  installed $$i in $(INSTALL_PREFIX)$(man5dir)" ; done
	@$(INSTALL_DATA) $(MAN8G) $(INSTALL_PREFIX)$(man8dir)
	@for i in $(MAN8G) ; do echo "install:  installed $$i in $(INSTALL_PREFIX)$(man8dir)" ; done

manuninstall:
	@for i in $(MAN1G) $(MAN1) ; do rm -f $(INSTALL_PREFIX)$(man1dir)/$$i ; echo "removed $$i from $(INSTALL_PREFIX)$(man1dir)" ; done
	@for i in $(MAN3G) $(MAN3) $(MANALIASES); do rm -f $(INSTALL_PREFIX)$(man3dir)/$$i ; echo "removed $$i from $(INSTALL_PREFIX)$(man3dir)" ; done
	@for i in $(MAN5G) ; do rm -f $(INSTALL_PREFIX)$(man5dir)/$$i ; echo "removed $$i from $(INSTALL_PREFIX)$(man5dir)" ; done
	@for i in $(MAN8G) ; do rm -f $(INSTALL_PREFIX)$(man8dir)/$$i ; echo "removed $$i from $(INSTALL_PREFIX)$(man8dir)" ; done

maninstalldirs:
	@$(SHELL) $(srcdir)/../mkinstalldirs $(INSTALL_PREFIX)$(man1dir) $(INSTALL_PREFIX)$(man3dir) $(INSTALL_PREFIX)$(man5dir) $(INSTALL_PREFIX)$(man8dir)


#
# internal administrative
#
html: $(MANALL)
	for i in $(MANALL); do \
#	   if test `wc -l $$i | awk '{print $$1}'` != 1 ; then \
		   base=`echo $$i | sed 's/.[0-9]$$//;'` ; \
		   echo "<HTML><BODY bgcolor=\"#ffffff\" background=\"../ucd-snmp-bg3.gif\"><PRE>" > $$base.html; \
		   man2html -r ./$$i | $(PERL) -p -e 's/HREF=\"..\/man.\//HREF=\"/g;s/\.[1-9]\.html/.html/g;' | grep -v 'Content-type:' >> $$base.html; \
		   a="$$a $$i"; \
#	   fi ; \
	done ;\
	$(PERL) make_index.pl man_sections.txt $$a > index.html

#
# standard target definitions.  Set appropriate variables to make use of them.
#
# note: the strange use of the "it" variable is for shell parsing when
# there is no targets to install for that rule.
#

# the standard items to build: libraries, bins, and sbins
STANDARDTARGETS     =$(INSTALLLIBS) $(INSTALLBINPROGS) $(INSTALLSBINPROGS)
STANDARDCLEANTARGETS=$(INSTALLLIBS) $(INSTALLPOSTLIBS) $(INSTALLBINPROGS) $(INSTALLSBINPROGS) $(INSTALLUCDLIBS)

standardall: subdirs $(STANDARDTARGETS)

objs: ${OBJS} ${LOBJS}

subdirs:
	@if test "$(SUBDIRS)" != ""; then \
		it="$(SUBDIRS)" ; \
		for i in $$it ; do \
			echo "making all in `pwd`/$$i"; \
			( cd $$i ; $(MAKE) ) ; \
			if test $$? != 0 ; then \
				exit 1 ; \
			fi  \
		done \
	fi

# installlibs handles local, ucd and subdir libs. need to do subdir libs
# before bins, sinze those libs may be needed for successful linking
install: installlocalheaders  \
         installlibs \
         installlocalbin      installlocalsbin   \
         installsubdirs      $(OTHERINSTALL)

uninstall: uninstalllibs uninstallbin uninstallsbin uninstallheaders \
           uninstallsubdirs $(OTHERUNINSTALL)

installprogs: installbin installsbin

#
# headers
#
# set INSTALLHEADERS to a list of things to install in each makefile.
# set INSTALLBUILTHEADERS to a list of things to install from builddir
# set INSTALLSUBDIRHEADERS and INSTALLSUBDIR to subdirectory headers
# set INSTALLSUBDIRHEADERS2 and INSTALLSUBDIR2 to more subdirectory headers
# set INSTALLBUILTSUBDIRHEADERS and INSTALLBUILTSUBDIR to a list from builddir
#
installheaders: installlocalheaders  installsubdirheaders

installlocalheaders:
	@if test "$(INSTALLHEADERS)" != "" ; then \
		echo creating directory $(INSTALL_PREFIX)$(includedir) ; \
		it="$(INSTALLHEADERS)" ; \
		$(SHELL) $(top_srcdir)/mkinstalldirs $(INSTALL_PREFIX)$(includedir) ; \
		for i in $$it ; do \
			$(INSTALL_DATA) $(top_srcdir)/include/net-snmp/$$i $(INSTALL_PREFIX)$(includedir) ; \
			echo "installing $$i in $(INSTALL_PREFIX)$(includedir)" ; \
		done \
	fi
	@if test "$(INSTALLBUILTHEADERS)" != "" ; then \
		echo creating directory $(INSTALL_PREFIX)$(includedir) ; \
		it="$(INSTALLBUILTHEADERS)" ; \
		$(SHELL) $(top_srcdir)/mkinstalldirs $(INSTALL_PREFIX)$(includedir) ; \
		for i in $$it ; do \
			$(INSTALL_DATA) $$i $(INSTALL_PREFIX)$(includedir) ; \
			echo "installing $$i in $(INSTALL_PREFIX)$(includedir)" ; \
		done \
	fi
	@if test "$(INCLUDESUBDIRHEADERS)" != "" ; then \
		echo creating directory $(INSTALL_PREFIX)$(includedir)/$(INCLUDESUBDIR) ; \
		it="$(INCLUDESUBDIRHEADERS)" ; \
		$(SHELL) $(top_srcdir)/mkinstalldirs $(INSTALL_PREFIX)$(includedir)/$(INCLUDESUBDIR) ; \
		for i in $$it ; do \
			$(INSTALL_DATA) $(top_srcdir)/include/net-snmp/$(INCLUDESUBDIR)/$$i $(INSTALL_PREFIX)$(includedir)/$(INCLUDESUBDIR) ; \
			echo "installing $$i in $(INSTALL_PREFIX)$(includedir)/$(INCLUDESUBDIR)" ; \
		done \
	fi
	@if test "$(INCLUDESUBDIRHEADERS2)" != "" ; then \
		echo creating directory $(INSTALL_PREFIX)$(includedir)/$(INCLUDESUBDIR2) ; \
		it="$(INCLUDESUBDIRHEADERS2)" ; \
		$(SHELL) $(top_srcdir)/mkinstalldirs $(INSTALL_PREFIX)$(includedir)/$(INCLUDESUBDIR2) ; \
		for i in $$it ; do \
			$(INSTALL_DATA) $(top_srcdir)/include/net-snmp/$(INCLUDESUBDIR2)/$$i $(INSTALL_PREFIX)$(includedir)/$(INCLUDESUBDIR2) ; \
			echo "installing $$i in $(INSTALL_PREFIX)$(includedir)/$(INCLUDESUBDIR2)" ; \
		done \
	fi
	@if test "$(INSTALLBUILTSUBDIRHEADERS)" != "" ; then \
		echo creating directory $(INSTALL_PREFIX)$(includedir)/$(INSTALLBUILTSUBDIR) ; \
		it="$(INSTALLBUILTSUBDIRHEADERS)" ; \
		$(SHELL) $(top_srcdir)/mkinstalldirs $(INSTALL_PREFIX)$(includedir)/$(INSTALLBUILTSUBDIR) ; \
		for i in $$it ; do \
			$(INSTALL_DATA) $$i $(INSTALL_PREFIX)$(includedir)/$(INSTALLBUILTSUBDIR) ; \
			echo "installing $$i in $(INSTALL_PREFIX)$(includedir)/$(INSTALLBUILTSUBDIR)" ; \
		done \
	fi

installucdheaders:
	@if test "$(INSTALLUCDHEADERS)" != "" ; then \
		echo creating directory $(INSTALL_PREFIX)$(ucdincludedir) ; \
		it="$(INSTALLUCDHEADERS)" ; \
		$(SHELL) $(top_srcdir)/mkinstalldirs $(INSTALL_PREFIX)$(ucdincludedir) ; \
		for i in $$it ; do \
			$(INSTALL_DATA) $(top_srcdir)/include/ucd-snmp/$$i $(INSTALL_PREFIX)$(ucdincludedir) ; \
			echo "installing $$i in $(INSTALL_PREFIX)$(ucdincludedir)" ; \
		done \
	fi

installsubdirheaders:
	@if test "$(SUBDIRS)" != ""; then \
		it="$(SUBDIRS)" ; \
		for i in $$it ; do \
			echo "making installheaders in `pwd`/$$i"; \
			( cd $$i ; $(MAKE) installheaders) ;   \
			if test $$? != 0 ; then \
				exit 1 ; \
			fi  \
		done \
	fi

uninstallheaders:
	@if test "$(INSTALLHEADERS)" != "" ; then \
		it="$(INSTALLHEADERS)" ; \
		for i in $$it ; do \
			rm -f $(INSTALL_PREFIX)$(includedir)/$$i ; \
			echo "removing $$i from $(INSTALL_PREFIX)$(includedir)" ; \
		done \
	fi
	@if test "$(INSTALLBUILTHEADERS)" != "" ; then \
		it="$(INSTALLBUILTHEADERS)" ; \
		for i in $$it ; do \
			rm -f $(INSTALL_PREFIX)$(includedir)/`basename $$i` ; \
			echo "removing $$i from $(INSTALL_PREFIX)$(includedir)" ; \
		done \
	fi
	@if test "$(INCLUDESUBDIRHEADERS)" != "" ; then \
		it="$(INCLUDESUBDIRHEADERS)" ; \
		for i in $$it ; do \
			rm -f $(INSTALL_PREFIX)$(includedir)/$(INCLUDESUBDIR)/$$i ; \
			echo "removing $$i from $(INSTALL_PREFIX)$(includedir)/$(INCLUDESUBDIR)" ; \
		done \
	fi
	@if test "$(INCLUDESUBDIRHEADERS2)" != "" ; then \
		it="$(INCLUDESUBDIRHEADERS2)" ; \
		for i in $$it ; do \
			rm -f $(INSTALL_PREFIX)$(includedir)/$(INCLUDESUBDIR2)/$$i ; \
			echo "removing $$i from $(INSTALL_PREFIX)$(includedir)/$(INCLUDESUBDIR2)" ; \
		done \
	fi
	@if test "$(INSTALLBUILTSUBDIRHEADERS)" != "" ; then \
		it="$(INSTALLBUILTSUBDIRHEADERS)" ; \
		for i in $$it ; do \
			rm -f $(INSTALL_PREFIX)$(includedir)/$(INSTALLBUILTSUBDIR)/`basename $$i` ; \
			echo "removing $$i from $(INSTALL_PREFIX)$(includedir)/$(INSTALLBUILTSUBDIR)" ; \
		done \
	fi

#
# libraries
#
# set INSTALLLIBS to a list of things to install in each makefile.
#
installlibs: installlocallibs  installsubdirlibs installpostlibs

installlocallibs: $(INSTALLLIBS)
	@if test "$(INSTALLLIBS)" != ""; then \
		it="$(INSTALLLIBS)" ; \
		$(SHELL) $(top_srcdir)/mkinstalldirs $(INSTALL_PREFIX)$(libdir) ; \
		$(INSTALL) $(INSTALLLIBS) $(INSTALL_PREFIX)$(libdir) ; \
		for i in $$it ; do \
			echo "installing $$i in $(INSTALL_PREFIX)$(libdir)"; \
			$(RANLIB) $(INSTALL_PREFIX)$(libdir)/$$i ; \
		done ; \
		$(LIB_LDCONFIG_CMD) ; \
	fi

installpostlibs: $(INSTALLPOSTLIBS)
	@if test "$(INSTALLPOSTLIBS)" != ""; then \
		it="$(INSTALLPOSTLIBS)" ; \
		$(SHELL) $(top_srcdir)/mkinstalldirs $(INSTALL_PREFIX)$(libdir) ; \
		$(INSTALL) $(INSTALLPOSTLIBS) $(INSTALL_PREFIX)$(libdir) ; \
		for i in $$it ; do \
			echo "installing $$i in $(INSTALL_PREFIX)$(libdir)"; \
			$(RANLIB) $(INSTALL_PREFIX)$(libdir)/$$i ; \
		done ; \
		$(LIB_LDCONFIG_CMD) ; \
	fi

installucdlibs: $(INSTALLUCDLIBS)
	@if test "$(INSTALLUCDLIBS)" != ""; then \
		it="$(INSTALLUCDLIBS)" ; \
		$(SHELL) $(top_srcdir)/mkinstalldirs $(INSTALL_PREFIX)$(libdir) ; \
		$(INSTALL) $(INSTALLUCDLIBS) $(INSTALL_PREFIX)$(libdir) ; \
		for i in $$it ; do \
			echo "installing $$i in $(INSTALL_PREFIX)$(libdir)"; \
			$(RANLIB) $(INSTALL_PREFIX)$(libdir)/$$i ; \
		done ; \
		$(LIB_LDCONFIG_CMD) ; \
	fi

installsubdirlibs:
	@if test "$(SUBDIRS)" != ""; then \
		it="$(SUBDIRS)" ; \
		for i in $$it ; do \
			echo "making installlibs in `pwd`/$$i"; \
			( cd $$i ; $(MAKE) installlibs) ;   \
			if test $$? != 0 ; then \
				exit 1 ; \
			fi  \
		done \
	fi

uninstalllibs:
	@if test "$(INSTALLLIBS)" != ""; then \
		it="$(INSTALLLIBS)" ; \
		for i in $$it ; do   \
			$(UNINSTALL) $(INSTALL_PREFIX)$(libdir)/$$i ; \
			echo "removing $$i from $(INSTALL_PREFIX)$(libdir)"; \
		done \
	fi

#
# normal bin binaries
#
# set INSTALLBINPROGS to a list of things to install in each makefile.
#
installbin: installlocalbin installsubdirbin

installlocalbin: $(INSTALLBINPROGS)
	@if test "$(INSTALLBINPROGS) $(INSTALLBINSCRIPTS)" != " "; then \
		$(SHELL) $(top_srcdir)/mkinstalldirs $(INSTALL_PREFIX)$(bindir) ; \
		it="$(INSTALLBINPROGS) $(INSTALLBINSCRIPTS)" ; \
		$(INSTALL) $(INSTALLBINPROGS) $(INSTALLBINSCRIPTS) $(INSTALL_PREFIX)$(bindir) ; \
		for i in $$it ; do   \
			echo "installing $$i in $(INSTALL_PREFIX)$(bindir)"; \
		done \
	fi

installsubdirbin:
	@if test "$(SUBDIRS)" != ""; then \
		it="$(SUBDIRS)" ; \
		for i in $$it ; do \
			echo "making installbin in `pwd`/$$i"; \
			( cd $$i ; $(MAKE) installbin) ;   \
			if test $$? != 0 ; then \
				exit 1 ; \
			fi  \
		done \
	fi

uninstallbin:
	@if test "$(INSTALLBINPROGS) $(INSTALLBINSCRIPTS)" != " "; then \
		it="$(INSTALLBINPROGS) $(INSTALLBINSCRIPTS)" ; \
		for i in $$it ; do   \
			$(UNINSTALL) $(INSTALL_PREFIX)$(bindir)/$$i ; \
			echo "removing $$i from $(INSTALL_PREFIX)$(bindir)"; \
		done \
	fi

#
# sbin binaries
#
# set INSTALLSBINPROGS to a list of things to install in each makefile.
#
installsbin: installlocalsbin installsubdirsbin

installlocalsbin: $(INSTALLSBINPROGS)
	@if test "$(INSTALLSBINPROGS)" != ""; then \
		it="$(INSTALLSBINPROGS)" ; \
		$(SHELL) $(top_srcdir)/mkinstalldirs $(INSTALL_PREFIX)$(sbindir) ; \
		$(INSTALL) $(INSTALLSBINPROGS) $(INSTALL_PREFIX)$(sbindir) ;  \
		for i in $$it ; do   \
			echo "installing $$i in $(INSTALL_PREFIX)$(sbindir)"; \
		done \
	fi

installsubdirsbin:
	@if test "$(SUBDIRS)" != ""; then \
		it="$(SUBDIRS)" ; \
		for i in $$it ; do \
			echo "making installsbin in `pwd`/$$i"; \
			( cd $$i ; $(MAKE) installsbin) ;   \
			if test $$? != 0 ; then \
				exit 1 ; \
			fi  \
		done \
	fi

uninstallsbin:
	@if test "$(INSTALLSBINPROGS)" != ""; then \
		it="$(INSTALLSBINPROGS)" ; \
		for i in $$it ; do   \
			$(UNINSTALL) $(INSTALL_PREFIX)$(sbindir)/$$i ; \
			echo "removing $$i from $(INSTALL_PREFIX)$(sbindir)"; \
		done \
	fi

#
# general make install target for subdirs
#
installsubdirs:
	@if test "$(SUBDIRS)" != ""; then \
		it="$(SUBDIRS)" ; \
		for i in $$it ; do \
			echo "making install in `pwd`/$$i"; \
			( cd $$i ; $(MAKE) install) ;   \
			if test $$? != 0 ; then \
				exit 1 ; \
			fi  \
		done \
	fi

uninstallsubdirs:
	@if test "$(SUBDIRS)" != ""; then \
		it="$(SUBDIRS)" ; \
		for i in $$it ; do \
			echo "making uninstall in `pwd`/$$i"; \
			( cd $$i ; $(MAKE) uninstall) ;   \
			if test $$? != 0 ; then \
				exit 1 ; \
			fi  \
		done \
	fi

#
# cleaning targets
#
clean: cleansubdirs $(OTHERCLEANTODOS)
	$(LIBTOOLCLEAN) ${OBJS} ${LOBJS} core $(STANDARDCLEANTARGETS) $(OTHERCLEANTARGETS)

cleansubdirs:
	@if test "$(SUBDIRS)" != ""; then \
		it="$(SUBDIRS)" ; \
		for i in $$it ; do \
			echo "making clean in `pwd`/$$i"; \
			( cd $$i ; $(MAKE) clean) ;   \
			if test $$? != 0 ; then \
				exit 1 ; \
			fi  \
		done \
	fi

lint:
	lint -nhx $(CSRCS)

#
# wacky dependency building.
#
depend: dependdirs
	@if test -f Makefile.depend ; then \
		makedepend `echo $(CPPFLAGS) | sed 's/-f[-a-z]*//g'` -o .lo $(srcdir)/*.c $(srcdir)/*/*.c ; \
	fi


nosysdepend: nosysdependdirs
	@if test -f Makefile.depend ; then \
		makedepend `echo $(CPPFLAGS) | sed 's/-f[-a-z]*//g'` -o .lo $(srcdir)/*.c $(srcdir)/*/*.c ; \
		$(PERL) -n -i.bak $(top_srcdir)/makenosysdepend.pl Makefile ; \
	fi

distdepend: nosysdepend distdependdirs
	@if test -f Makefile.depend ; then \
		$(PERL) $(top_srcdir)/makefileindepend.pl ; \
	fi

dependdirs:
	@if test "$(SUBDIRS)" != ""; then \
		it="$(SUBDIRS)" ; \
		for i in $$it ; do \
			echo "making depend in `pwd`/$$i"; \
			( cd $$i ; $(MAKE) depend) ;   \
			if test $$? != 0 ; then \
				exit 1 ; \
			fi  \
		done \
	fi

nosysdependdirs:
	@if test "$(SUBDIRS)" != ""; then \
		it="$(SUBDIRS)" ; \
		for i in $$it ; do \
			echo "making nosysdepend in `pwd`/$$i"; \
			( cd $$i ; $(MAKE) nosysdepend) ;   \
			if test $$? != 0 ; then \
				exit 1 ; \
			fi  \
		done \
	fi

distdependdirs:
	@if test "$(SUBDIRS)" != ""; then \
		it="$(SUBDIRS)" ; \
		for i in $$it ; do \
			echo "making distdepend in `pwd`/$$i"; \
			( cd $$i ; $(MAKE) distdepend) ;   \
			if test $$? != 0 ; then \
				exit 1 ; \
			fi  \
		done \
	fi

# These aren't real targets, let gnu's make know that.
.PHONY: clean cleansubdirs lint \
	install installprogs installheaders installlibs \
	installbin installsbin installsubdirs \
	all subdirs standardall objs \
	depend nosysdepend distdepend dependdirs nosysdependdirs distdependdirs
