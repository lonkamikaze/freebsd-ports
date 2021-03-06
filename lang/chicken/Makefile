# Created by: Kimura Fuyuki <fuyuki@hadaly.org>
# $FreeBSD$

PORTNAME=	chicken
PORTVERSION=	4.10.0
PORTEPOCH=	1
CATEGORIES=	lang scheme
MASTER_SITES=	http://code.call-cc.org/releases/${PORTVERSION}/

MAINTAINER=	vmagerya@gmail.com
COMMENT=	Scheme-to-C compiler

USES=		cpe gmake
CPE_VENDOR=	call-cc
MAKEFILE=	GNUmakefile
USE_LDCONFIG=	yes
MAKE_ARGS+=	PLATFORM=bsd \
		PREFIX=${PREFIX} \
		MANDIR=${PREFIX}/man \
		LIBDIR="${PREFIX}/lib" \
		DOCDIR="${DOCSDIR}" \
		ARCH=${NEW_ARCH} \
		C_COMPILER=${CC:Q} \
		CXX_COMPILER=${CXX:Q} \
		LIBRARIAN="${AR}" \
		C_COMPILER_OPTIMIZATION_OPTIONS="${CFLAGS}"

NEW_ARCH=	${ARCH:S/i386/x86/:S/amd64/x86-64/}

OPTIONS_DEFINE=	DOCS

.include <bsd.port.pre.mk>

.if ${ARCH} != "amd64" && ${ARCH} != "i386" && ${ARCH} != "sparc64"
MAKE_ARGS+=	HACKED_APPLY=
.endif

post-install:
	${INSTALL_DATA} ${WRKSRC}/NEWS ${STAGEDIR}${DOCSDIR}
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/*
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/chicken/7/*.so
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/libchicken*

# This only works *after* chicken is installed.
regression-test: build
	(cd ${BUILD_WRKSRC}; ${SETENV} ${MAKE_ENV} \
		${MAKE_CMD} ${MAKE_FLAGS} ${MAKEFILE} ${MAKE_ARGS} check)

.include <bsd.port.post.mk>
