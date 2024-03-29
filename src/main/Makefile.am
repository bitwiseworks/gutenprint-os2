## Copyright (C) 2000 Roger Leigh
##
## This program is free software; you can redistribute it and/or modify
## it under the terms of the GNU General Public License as published by
## the Free Software Foundation; either version 2, or (at your option)
## any later version.
##
## This program is distributed in the hope that it will be useful,
## but WITHOUT ANY WARRANTY; without even the implied warranty of
## MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
## GNU General Public License for more details.
##
## You should have received a copy of the GNU General Public License
## along with this program.  If not, see <https://www.gnu.org/licenses/>.

## Process this file with automake to produce Makefile.in.

@SET_MAKE@

include $(top_srcdir)/scripts/global.mk


## Variables

VENDOR ?=community
BUILD_INFO=\#\#1\#\# $(shell date +'%d %b %Y %H:%M:%S')     $(shell uname -n)
BUILDLEVEL_INFO=@\#$(VENDOR):$(GUTENPRINT_VERSION)\#@$(BUILD_INFO)::::$(GUTENPRINT_MICRO_VERSION)::

pkgconfigdatadir = $(libdir)/pkgconfig
pkgmoduledir = $(pkglibdir)/@GUTENPRINT_MAJOR_VERSION@.@GUTENPRINT_MINOR_VERSION@/modules


## Programs

# So we can maintainerclean these files even if
# modules aren't (currently) in use.
pkg_libraries = \
	color-traditional.la \
	print-canon.la \
	print-escp2.la \
	print-lexmark.la \
	print-pcl.la \
	print-dpl.la \
	print-ps.la \
	print-dyesub.la \
	print-raw.la

if BUILD_MODULES
pkgmodule_LTLIBRARIES = \
	$(pkg_libraries)
endif

color_traditional_la_SOURCES = \
	print-color.c \
	color-conversion.h \
	color-conversions.c

color_traditional_la_LDFLAGS = -module -avoid-version

print_canon_la_SOURCES = \
	print-canon.c \
	print-canon.h \
	canon-inks.h \
	canon-media.h \
	canon-modes.h \
	canon-printers.h \
	canon-media-mode.h

print_canon_la_LDFLAGS = -module -avoid-version

print_escp2_la_SOURCES = \
	print-escp2.c \
	escp2-driver.c \
	print-escp2.h \
	print-escp2-data.c \
	escp2-channels.c \
	escp2-papers.c \
	escp2-resolutions.c
print_escp2_la_LDFLAGS = -module -avoid-version

print_lexmark_la_SOURCES = print-lexmark.c
print_lexmark_la_LDFLAGS = -module -avoid-version

print_pcl_la_SOURCES = print-pcl.c
print_pcl_la_LDFLAGS = -module -avoid-version

print_dpl_la_SOURCES = print-dpl.c
print_dpl_la_LDFLAGS = -module -avoid-version

print_ps_la_SOURCES = print-ps.c xmlppd.c xmlppd.h
print_ps_la_LDFLAGS = -module -avoid-version

print_dyesub_la_SOURCES = print-dyesub.c
print_dyesub_la_LDFLAGS = -module -avoid-version

print_raw_la_SOURCES = print-raw.c
print_raw_la_LDFLAGS = -module -avoid-version

lib_LTLIBRARIES = libgutenprint.la

module_SOURCES =				\
	$(color_traditional_la_SOURCES)		\
	$(print_canon_la_SOURCES)		\
	$(print_escp2_la_SOURCES)		\
	$(print_lexmark_la_SOURCES)		\
	$(print_pcl_la_SOURCES)			\
	$(print_dpl_la_SOURCES)			\
	$(print_ps_la_SOURCES)			\
	$(print_dyesub_la_SOURCES)		\
	$(print_raw_la_SOURCES)

if !BUILD_MODULES
libgutenprint_modules = $(module_SOURCES)
endif

mxml_SOURCES =					\
	mxml-attr.c				\
	mxml-file.c				\
	mxml-node.c				\
	mxml-search.c

libgutenprint_headers =				\
	dither-impl.h				\
	dither-inlined-functions.h		\
	generic-options.h			\
	gutenprint-internal.h

libgutenprint_la_SOURCES =			\
	array.c					\
	bit-ops.c				\
	channel.c				\
	color.c					\
	curve.c					\
	curve-cache.c				\
	dither-ed.c				\
	dither-eventone.c			\
	dither-inks.c				\
	dither-main.c				\
	dither-ordered.c			\
	dither-very-fast.c			\
	dither-predithered.c			\
	generic-options.c			\
	image.c					\
	buffer-image.c				\
	module.c				\
	path.c					\
	print-dither-matrices.c			\
	print-list.c				\
	print-papers.c				\
	print-util.c				\
	print-vars.c				\
	print-version.c				\
	print-weave.c				\
	printers.c				\
	refcache.c				\
	sequence.c				\
	string-list.c				\
	xml.c					\
	$(mxml_SOURCES)				\
	$(libgutenprint_headers)		\
	$(libgutenprint_modules)

libgutenprint_la_LIBADD = $(GUTENPRINT_LIBDEPS)
# Uncommment to build an unversioned library (version in soname)
#libgutenprint_version = -release $(GUTENPRINT_VERSION)
# Uncomment to build a versioned library
libgutenprint_version = -version-info $(GUTENPRINT_CURRENT_INTERFACE):$(GUTENPRINT_INTERFACE_AGE):$(GUTENPRINT_BINARY_AGE)
libgutenprint_la_LDFLAGS = $(libgutenprint_version) \
	-buildlevel '$(BUILDLEVEL_INFO)'	\
	-rpath $(libdir) -no-undefined
# libtool currently needs a patch for symbol export to work correctly
# using a linker version script.
#	-export-symbols $(srcdir)/libgutenprint.sym


## Data

pkgconfigdata_DATA = gutenprint.pc


## Clean

MAINTAINERCLEANFILES = Makefile.in $(pkg_libraries)

EXTRA_DIST = libgutenprint.sym
