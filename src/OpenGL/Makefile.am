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

noinst_LTLIBRARIES = libopengl_main.la
libopengl_main_la_SOURCES = libopengl.c
libopengl_main_la_CFLAGS = \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/src/GLdispatch/vnd-glapi \
	-I$(top_srcdir)/src/GLdispatch/ \
	-I$(top_srcdir)/src/util


lib_LTLIBRARIES = libOpenGL.la

libOpenGL_la_SOURCES =
libOpenGL_la_LDFLAGS = -shared \
	$(LINKER_FLAG_NO_UNDEFINED) \
	-version-info 0

libOpenGL_la_LIBADD = \
	libopengl_main.la \
	../GLdispatch/libGLdispatch.la \
	../GLdispatch/vnd-glapi/libglapi_opengl.la \
	../util/libutils_misc.la

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = opengl.pc

AM_TESTS_ENVIRONMENT = \
	TOP_SRCDIR='$(top_srcdir)' \
	TOP_BUILDDIR='$(top_builddir)' \
	NM='$(NM)' \
	PYTHON='$(PYTHON)'
TESTS = ogl-symbol-check.sh

EXTRA_DIST = \
	ogl-symbol-check.sh \
	ogl.symbols \
	meson.build
