# Process this file with autoconf to produce a configure script.

GEDIT_MAJOR=2.16.0
GEDIT_PLUGINS_MAJOR=2.18.0

AC_INIT(gedit-plugins, 2.18.0, http://bugzilla.gnome.org/enter_bug.cgi?product=gedit)

AC_CONFIG_SRCDIR([dictionary])
AC_CONFIG_MACRO_DIR([m4])
AC_PREFIX_PROGRAM([gedit])

AC_SUBST(GEDIT_PLUGINS_MAJOR)

AC_PREREQ(2.59)

AM_INIT_AUTOMAKE([1.8 dist-bzip2 no-dist-gzip])

GNOME_DOC_INIT

AM_MAINTAINER_MODE
AC_CONFIG_HEADERS([config.h])
AC_DISABLE_STATIC

AC_PATH_PROG(GCONFTOOL, gconftool-2)
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

GETTEXT_PACKAGE=gedit-plugins
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE,"$GETTEXT_PACKAGE", [Gettext package])
AM_GLIB_GNU_GETTEXT

# ================================================================
# Start of pkg-config checks
# ================================================================

PKG_CHECK_MODULES(GEDIT, [
	glib-2.0 >= 2.8.0
	gtk+-2.0 >= 2.8.0
	gtksourceview-1.0 >= 1.2.0
	gedit-2.16 >= 2.16.0
	libglade-2.0 >= 2.4.0
	gnome-vfs-2.0 >= 2.13.4
	gdict-1.0 >= 0.10.8
])
GEDIT_LIBS="${GEDIT_LIBS}"
AC_SUBST(GEDIT_LIBS)
AC_SUBST(GEDIT_CFLAGS)

# ================================================================
# Plugins
# ================================================================

# ================================================================
# dictionary
# ================================================================
plugin_defined dictionary
if test "$?" = 1
then
	PKG_CHECK_MODULES([DICT], [
		gdict-1.0 >= 0.10.8
	], have_dictionary=yes, have_dictionary=no)
	
	if test "x$have_dictionary" = "xno"
	then
		plugin_defined_explicit dictionary
		if test "$?" = 1
		then
			AC_MSG_ERROR([dictionary could not be found, needed to built dictionary plugin])
		else
			AC_MSG_WARN([dictionary could not be found, dictionary plugin will be disabled])

			undef_plugin dictionary "dictionary not found"
		fi
	fi
fi

# ================================================================
# Misc
# ================================================================
AC_PATH_PROG(GLIB_GENMARSHAL, glib-genmarshal)
			      
#GNOME_COMPILE_WARNINGS(yes)

AC_ARG_ENABLE(deprecations,
              [AC_HELP_STRING([--enable-deprecations],
                              [warn about deprecated usages [default=no]])],,
              [enable_deprecations=no])

if test "x$enable_deprecations" = "xyes"
then
	DISABLE_DEPRECATED_CFLAGS="\
		-DG_DISABLE_DEPRECATED		\
		-DGDK_DISABLE_DEPRECATED	\
		-DGTK_DISABLE_DEPRECATED	\
		-DGDK_PIXBUF_DISABLE_DEPRECATED	\
		-DGNOME_DISABLE_DEPRECATED"
	AC_SUBST(DISABLE_DEPRECATED_CFLAGS)
fi

PLUGIN_LIBTOOL_FLAGS="-module -avoid-version"
AC_SUBST(PLUGIN_LIBTOOL_FLAGS)

AC_CONFIG_FILES([
Makefile
dictionary/Makefile
po/Makefile.in])

AC_OUTPUT

