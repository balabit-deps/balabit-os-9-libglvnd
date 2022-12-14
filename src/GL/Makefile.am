# Copyright (c) 2013, NVIDIA CORPORATION.
#
# Permission is hereby granted, free of charge, to any person obtaining a
# copy of this software and/or associated documentation files (the
# "Materials"), to deal in the Materials without restriction, including
# without limitation the rights to use, copy, modify, merge, publish,
# distribute, sublicense, and/or sell copies of the Materials, and to
# permit persons to whom the Materials are furnished to do so, subject to
# the following conditions:
#
# The above copyright notice and this permission notice shall be included
# unaltered in all copies or substantial portions of the Materials.
# Any additions, deletions, or changes to the original source files
# must be clearly indicated in accompanying documentation.
#
# THE MATERIALS ARE PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
# EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
# MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
# IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
# CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
# TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
# MATERIALS OR THE USE OR OTHER DEALINGS IN THE MATERIALS.

lib_LTLIBRARIES = libGL.la

TOP = $(top_srcdir)
MAPI = $(top_srcdir)/$(MAPI_PREFIX)
GLAPI = $(MAPI)/glapi

include $(top_srcdir)/src/GLdispatch/vnd-glapi/entry_files.mk

libGL_la_SOURCES =      \
	libgl.c             \
	g_libglglxwrapper.c

if HAVE_PYTHON
BUILT_SOURCES = g_libglglxwrapper.c
CLEANFILES = $(BUILT_SOURCES)

glapi_gen_glx_xml := \
	$(top_srcdir)/src/generate/xml/glx.xml \
	$(top_srcdir)/src/generate/xml/glx_other.xml
glapi_gen_libglglxstubs_script = $(top_srcdir)/src/generate/gen_libgl_glxstubs.py
glapi_gen_libglglxstubs_deps = \
	$(glapi_gen_libglglxstubs_script) \
	$(top_srcdir)/src/generate/genCommon.py \
	$(glapi_gen_glx_xml)

g_libglglxwrapper.c : $(glapi_gen_libglglxstubs_deps)
	$(AM_V_GEN)$(PYTHON) $(PYTHON_FLAGS) $(glapi_gen_libglglxstubs_script) $(glapi_gen_glx_xml) > $@
endif

AM_TESTS_ENVIRONMENT = \
	TOP_SRCDIR='$(top_srcdir)' \
	TOP_BUILDDIR='$(top_builddir)' \
	NM='$(NM)' \
	PYTHON='$(PYTHON)'
TESTS = gl-symbol-check.sh

libGL_la_CFLAGS = \
	-I$(top_srcdir)/include

libGL_la_LDFLAGS = -shared -version-info 8:0:7 $(LINKER_FLAG_NO_UNDEFINED)

AM_CPPFLAGS = \
	-I$(TOP)/src/GLdispatch/vnd-glapi \
	-I$(TOP)/src/GLX \
	-I$(TOP)/src/GLdispatch \
	-I$(TOP)/src/util

libGL_la_LIBADD  = ../GLX/libGLX.la
libGL_la_LIBADD += ../GLdispatch/libGLdispatch.la
libGL_la_LIBADD += ../GLdispatch/vnd-glapi/libglapi_gl.la
libGL_la_LIBADD += ../util/libutils_misc.la
libGL_la_LIBADD += @LIB_DL@

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = gl.pc

EXTRA_DIST = \
	gl-symbol-check.sh \
	gl.symbols \
	meson.build
