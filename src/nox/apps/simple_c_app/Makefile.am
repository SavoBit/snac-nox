include ../../../Make.vars 

EXTRA_DIST =\
	meta.xml

if PY_ENABLED
AM_CPPFLAGS += $(PYTHON_CPPFLAGS)
endif # PY_ENABLED 

pkglib_LTLIBRARIES =		\
	simple_cc_app.la

simple_cc_app_la_CPPFLAGS = $(AM_CPPFLAGS) -I $(top_srcdir)/src/nox -I $(top_srcdir)/src/nox/apps/
simple_cc_app_la_SOURCES = simple_cc_app.cc
simple_cc_app_la_LDFLAGS = -module -export-dynamic

NOX_RUNTIMEFILES = meta.xml	

all-local: nox-all-local
clean-local: nox-clean-local 
install-exec-hook: nox-install-local
