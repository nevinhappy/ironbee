include $(top_srcdir)/build/tests.mk

if THREAD_SANITIZER_WORKAROUND
else

LDADD = \
	-lluajit-ironbee \
    $(top_builddir)/tests/ibtest_util.o \
	$(top_builddir)/util/libibutil.la
AM_LDFLAGS += \
	-L$(abs_top_builddir)/libs/luajit-2.0-ironbee/src \
    -L$(top_builddir)/util
AM_CPPFLAGS += \
    -I$(top_srcdir)/tests \
    -DTOP_SRCDIR=$(top_srcdir)

if DARWIN
# On Darwin (OSX) this is necessary for LuaJIT to run properly.
AM_LDFLAGS += -pagezero_size 10000 -image_base 100000000
endif

TESTS             = $(check_PROGRAMS)

EXTRA_DIST = \
	tc_testing.rb \
	ts_all.rb \
	waggle01.lua

check_PROGRAMS    = test_lua \
                    test_lua_json
test_lua_SOURCES  = test_lua.cpp \
                    test_lua_ibcutil.cpp
test_lua_CPPFLAGS = \
    -I$(top_srcdir)/libs/luajit-2.0-ironbee/src \
    $(AM_CPPFLAGS)

test_lua_json_SOURCES  = test_lua_json.cpp
test_lua_json_CPPFLAGS = \
	-I$(top_srcdir)/libs/luajit-2.0-ironbee/src \
	$(AM_CPPFLAGS)

check-local: check-ruby

endif
