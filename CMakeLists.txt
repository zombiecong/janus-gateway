cmake_minimum_required(VERSION 3.5)
project(janus)

set(SOURCE_FILES debug.h rtp.h mach_gettime.h mutex.h transports/transport.h
        log.c log.h
        utils.c utils.h
        config.c config.h
        ${_header} ${_out}
        rtcp.c rtcp.h
        sdp.c sdp.h
        dtls-bio.c dtls-bio.h
        janus.c janus.h
        dtls.c dtls.h
        sctp.c sctp.h
        ice.c ice.h
        auth.c auth.h
        turnrest.c turnrest.h
        plugins/plugin.h plugins/plugin.c
        apierror.c apierror.h )

include(FindPkgConfig)
pkg_check_modules(GLIB2 glib-2.0 REQUIRED)
pkg_check_modules(GOBJECT2 gobject-2.0 REQUIRED)
pkg_check_modules(NICE nice REQUIRED)

pkg_check_modules(MICROHTTPD libmicrohttpd REQUIRED)
pkg_check_modules(SRTP libsrtp REQUIRED)
pkg_check_modules(SIP sofia-sip-ua REQUIRED)
pkg_check_modules(JANSSON jansson REQUIRED)
pkg_check_modules(LIBSSL libssl REQUIRED)

include_directories(${GLIB2_INCLUDE_DIRS})
include_directories(${MICROHTTPD_INCLUDE_DIRS})
include_directories(${NICE_INCLUDE_DIRS})
include_directories(${SRTP_INCLUDE_DIRS})
include_directories(${SIP_INCLUDE_DIRS})
include_directories(${OPENSSL_INCLUDE_DIRS})

add_executable(janus ${SOURCE_FILES})