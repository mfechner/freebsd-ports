# Created by: gahr
# $FreeBSD$

PORTNAME=	tcl
DISTVERSION=	8.7.a0.20170426
PORTREVISION=	1
CATEGORIES=	lang
MASTER_SITES=	http://core.tcl.tk/tcl/tarball/
PKGNAMESUFFIX=	${PORTVERSION:R:R:S/.//}
DISTFILES=	Tcl+Source+Code${EXTRACT_SUFX}?uuid=${FOSSIL_CHECKIN}

MAINTAINER=	tcltk@FreeBSD.org
COMMENT=	Tool Command Language

LICENSE=	TclTk
LICENSE_NAME=	Tcl/Tk License
LICENSE_FILE=	${WRKSRC}/../license.terms
LICENSE_PERMS=	dist-mirror dist-sell pkg-mirror pkg-sell auto-accept

OPTIONS_DEFINE=	TCLMAN TZDATA MODULES THREADS DEBUG
OPTIONS_DEFINE_amd64=	DTRACE
OPTIONS_DEFAULT=MODULES THREADS
OPTIONS_DEFAULT_amd64=	DTRACE
TCLMAN_DESC=	Install Tcl function manpages
TZDATA_DESC=	Install Tcl timezone data
MODULES_DESC=	Install Tcl common modules
OPTIONS_SUB=	yes

.if !exists(/usr/sbin/dtrace)
OPTIONS_EXCLUDE+=	DTRACE
.endif

OPTIONS_EXCLUDE_FreeBSD_10=	DTRACE

FOSSIL_CHECKIN=	f590914719

PATCH_WRKSRC=	${WRKDIR}/Tcl_Source_Code
WRKSRC=		${PATCH_WRKSRC}/unix

ALL_TARGET=	all
INSTALL_TARGET=	install-strip install-libraries
TEST_TARGET=	test-tcl

USE_LDCONFIG=	yes
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--enable-shared \
		--enable-man-suffix=.${MAN_SUFFIX} \
		--includedir=${PREFIX}/include/tcl${TCL_VER} \
		--enable-symbols
CONFIGURE_ENV=	PORTSDIR=${PORTSDIR}

TCL_VER=	${PORTVERSION:R:R}
MAN_SUFFIX=	${PKGBASE}

MAKE_ENV=	SHORT_TCL_VER=${PKGNAMESUFFIX} \
		MAN_SUFFIX=.${MAN_SUFFIX}

PLIST_SUB=	TCL_VER=${TCL_VER} \
		PKGNAMESUFFIX=${PKGNAMESUFFIX}

TCLMAN_INSTALL_TARGET=	install-doc
TZDATA_INSTALL_TARGET=	install-tzdata
MODULES_INSTALL_TARGET=	install-modules
THREADS_CONFIGURE_ENABLE=	threads
DEBUG_CONFIGURE_ENABLE=	symbols
DTRACE_CONFIGURE_ENABLE=	dtrace

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MDTRACE}
PLIST_SUB+=	DTRACE=""
.else
PLIST_SUB+=	DTRACE="@comment "
.endif

post-patch:
	${REINPLACE_CMD} -e \
	    's|@TCL_BUILD_LIB_SPEC@|@TCL_LIB_SPEC@|; \
	     s|@TCL_BUILD_STUB_LIB_SPEC@|@TCL_STUB_LIB_SPEC@|; \
	     s|@TCL_BUILD_STUB_LIB_PATH@|@TCL_STUB_LIB_PATH@|; \
	     s|@TCL_SRC_DIR@|${PREFIX}/include/tcl${TCL_VER}|' \
	     ${PATCH_WRKSRC}/unix/tclConfig.sh.in

post-patch-TCLMAN-off:
	@${FIND} ${PATCH_WRKSRC}/pkgs -name Makefile.in | ${XARGS} ${REINPLACE_CMD} \
	    -e '/^install:/s|install-doc||'

post-configure:
	${REINPLACE_CMD} \
		-e 's,-DNO_MEMMOVE=1,,' -e 's,-DNO_STRING_H=1,,' \
		-e 's,^COMPAT_OBJS.*,,' ${WRKSRC}/Makefile

.include <bsd.port.mk>
