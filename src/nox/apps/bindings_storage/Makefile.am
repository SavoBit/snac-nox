include ../../../Make.vars 

EXTRA_DIST = meta.xml		\
	__init__.py \
	bindings_directory.py \
	bind_stuff_test.py \
	pybindings_storage.i

if PY_ENABLED

AM_CPPFLAGS += $(PYTHON_CPPFLAGS)

endif # PY_ENABLED 

pkglib_LTLIBRARIES = \
	bindings_storage.la \
	bs_memleak_test.la

bindings_storage_la_CPPFLAGS =						\
	$(AM_CPPFLAGS)							\
	-I $(top_srcdir)/src/nox					\
	-I $(top_srcdir)/src/nox/apps/					\
	-D__COMPONENT_FACTORY_FUNCTION__=bindings_storage_get_factory
bindings_storage_la_SOURCES = bindings_storage.cc  bindings_storage.hh serial_op_queue.hh 
bindings_storage_la_LDFLAGS = -module -export-dynamic

bs_memleak_test_la_CPPFLAGS =						\
	$(AM_CPPFLAGS)							\
	-I $(top_srcdir)/src/nox					\
	-I $(top_srcdir)/src/nox/apps/					\
	-D__COMPONENT_FACTORY_FUNCTION__=bs_memleak_test_get_factory
bs_memleak_test_la_SOURCES = bs_memleak_test.cc 
bs_memleak_test_la_LDFLAGS = -module -export-dynamic

NOX_RUNTIMEFILES = meta.xml	

if PY_ENABLED

AM_CPPFLAGS += $(PYTHON_CPPFLAGS)
NOX_RUNTIMEFILES += __init__.py \
								bindings_directory.py \
								bind_stuff_test.py

NOX_PYBUILDFILES = pybindings_storage.py								

pybindings_storage_wrap.cc pybindings_storage.py: pybindings_storage.i bs_datastructures.i 
		swig -I$(top_srcdir)/src/nox/lib/ -outdir $(builddir)/. -o pybindings_storage_wrap.cc -c++ -python -module pybindings_storage $(srcdir)/pybindings_storage.i

pkglib_LTLIBRARIES += _pybindings_storage.la
_pybindings_storage_la_CPPFLAGS = $(AM_CPPFLAGS) -I$(top_srcdir)/src/nox -I$(srcdir)/../ -I$(top_builddir)/src/nox/
_pybindings_storage_la_SOURCES = bindings_storage_proxy.cc bindings_storage_proxy.hh bs_datastructures.i
nodist__pybindings_storage_la_SOURCES = pybindings_storage_wrap.cc
_pybindings_storage_la_LDFLAGS = -module

NOX_PYLIBFILES = \
	_pybindings_storage.so 

endif # PY_ENABLED

all-local:  nox-all-local
clean-local: nox-clean-local
install-exec-hook: nox-install-local
