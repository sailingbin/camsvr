#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.63])
AC_INIT(camera-server,0.1,zergwangj@163.com)
AM_INIT_AUTOMAKE(camera-server,0.1)
AC_CONFIG_SRCDIR([CameraServer.cpp])
AC_CONFIG_HEADERS([config.h])

# Checks for programs.
if test -z $CXXFLAGS; then
    CXXFLAGS=''
fi
if test -z $CFLAGS; then
    CFLAGS=''
fi
AC_PROG_CXX
AC_PROG_CC

# Checks for libraries.
AC_CHECK_LIB(v4l2,v4l2_open,,AC_MSG_WARN(v4l2.a may be required for capture video))
AC_CHECK_LIB(x264,x264_predict_16x16_init)
AC_CHECK_LIB(avutil,av_malloc,,AC_MSG_WARN(libavutil.a may be required for MPEG streaming))
AC_CHECK_LIB(avcodec,avcodec_register_all,,AC_MSG_WARN(libavcodec.a is required for MPEG streaming))
AC_CHECK_LIB(avformat,avformat_new_stream,,AC_MSG_WARN(libavformat.a is required for MPEG streaming))
AC_CHECK_LIB(avfilter,avfilter_get_by_name,,AC_MSG_WARN(libavfilter.a is required for MPEG streaming))
AC_CHECK_LIB(avdevice,avdevice_register_all,,AC_MSG_WARN(libavdevice.a may be required for MPEG streaming))
AC_CHECK_LIB(swscale,sws_scale,,,-lswscale)
AC_CHECK_LIB(pthread,pthread_create,,AC_MSG_WARN(libpthread.a is required))
AC_CHECK_LIB(freetype,FT_Init_FreeType,,AC_MSG_WARN(libfreetype.a is required))

# Checks for header files.
AC_CHECK_HEADERS([libavcodec/avcodec.h libavformat/avformat.h libswscale/swscale.h libavdevice/avdevice.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_TYPE_UINT8_T

# Checks for library functions.
AC_CHECK_FUNCS([memset])

# Enable debug compiler flags.
AC_ARG_ENABLE([debug],
[AS_HELP_STRING([--enable-debug], [enable debugging, default: no])],
[case "${enableval}" in
	yes) IS_DEBUG=true ;;
	no)  IS_DEBUG=false ;;
	*) AC_MSG_ERROR([bad value ${enableval} for --enable-debug]) ;;
esac],
[IS_DEBUG=false])

if test "$IS_DEBUG" = true
then
#	AC_DEFINE([IS_DEBUG], [1], [Debug])
#	AC_SUBST([IS_DEBUG], [true])
#	AC_SUBST([DEBUG_PREFIX], [])
	AM_CONDITIONAL([IS_DEBUG], [true])
	AC_MSG_NOTICE([debug mode is enable])
else
#	AC_DEFINE([IS_DEBUG], [0], [Debug])
#	AC_SUBST([IS_DEBUG], [false])
#	AC_SUBST([DEBUG_PREFIX], [@])
	AM_CONDITIONAL([IS_DEBUG], [false])
	AC_MSG_NOTICE([debug mode is disable])
fi

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
