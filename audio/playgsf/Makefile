# Created by: Emanuel Haupt <ehaupt@critical.ch>
# $FreeBSD$

PORTNAME=	playgsf
PORTVERSION=	0.7.1
PORTREVISION=	2
CATEGORIES=	audio
MASTER_SITES=	http://projects.raphnet.net/playgsf/ \
		LOCAL/ehaupt

MAINTAINER=	ehaupt@FreeBSD.org
COMMENT=	Command-line player for gsf audio files

LIB_DEPENDS=	libao.so:audio/libao

USES=		gmake dos2unix
GNU_CONFIGURE=	yes

CFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib

CONFIGURE_ARGS+=	--enable-ccore --disable-optimisations

PLIST_FILES=	bin/playgsf

ONLY_FOR_ARCHS=	i386 amd64

PORTSCOUT=	skipv:0.7.2

post-patch:
	@${REINPLACE_CMD} \
		-e 's|\([[:space:]]*\).*configure.*|\1@true|' \
			${WRKSRC}/Makefile.in
	@${REINPLACE_CMD} \
		-e '/^CFLAGS="-DLINUX/s|"$$| ${CFLAGS}"|' \
		-e '/^LDFLAGS="-lz/s|"$$| ${LDFLAGS}"|' \
		${WRKSRC}/configure

post-configure:
	@(cd ${WRKSRC}/libresample-0.1.3 && ${SETENV} \
		CC=${CC:Q} CPP=${CPP:Q} CXX=${CXX:Q} \
		CFLAGS="${CFLAGS}" CPPFLAGS="${CPPFLAGS}" CXXFLAGS="${CXXFLAGS}" \
		${CONFIGURE_ENV} ./configure)

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin

.include <bsd.port.mk>
