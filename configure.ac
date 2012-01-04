# Process this file with autoconf to produce a configure script.

AC_INIT(gedit-dictionary, 3.0.0, http://bugzilla.gnome.org/enter_bug.cgi?product=gedit)

AC_CONFIG_SRCDIR([dictionary])
AC_CONFIG_MACRO_DIR([m4])
AC_PREFIX_PROGRAM([gedit])

AC_PREREQ(2.59)

AM_INIT_AUTOMAKE([1.8 dist-bzip2 no-dist-gzip])

AC_CONFIG_HEADERS([config.h])
AC_DISABLE_STATIC

IT_PROG_INTLTOOL([0.35.0])

AC_PROG_LIBTOOL

AC_ISC_POSIX
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_MAKE_SET

# make sure we keep ACLOCAL_FLAGS around for maintainer builds to work
AC_SUBST(ACLOCAL_AMFLAGS, "$ACLOCAL_FLAGS -I m4")

# ================================================================
# Gettext stuff.
# ================================================================

GETTEXT_PACKAGE=gedit-dictionary
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE,"$GETTEXT_PACKAGE", [Gettext package])
AM_GLIB_GNU_GETTEXT

# ================================================================
# Start of pkg-config checks
# ================================================================

PKG_CHECK_MODULES(GEDIT_DICTIONARY, [
	glib-2.0 >= 2.8.0
	gtk+-3.0 >= 2.8.0
	gedit-3.0 >= 2.16.0
	gdict-1.0 >= 0.10.8
])

AC_CONFIG_FILES([
Makefile
dictionary/Makefile
po/Makefile.in])

AC_OUTPUT

