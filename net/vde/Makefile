# Created by: Craig Boston <craig@yekse.gank.org>
# $FreeBSD$

PORTNAME=	vde
PORTVERSION=	1.5.7
CATEGORIES=	net
MASTER_SITES=	SF/${PORTNAME}/OldFiles

MAINTAINER=	ports@FreeBSD.org
COMMENT=	User-mode virtual ethernet infrastructure

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/COPYING

CONFLICTS=	vde2-[0-9]*

MAKE_ARGS=	CC=${CC:Q}
USE_LDCONFIG=	yes
USE_CSTD=	gnu89
USES=		gmake tar:tgz

CFLAGS+=	-fPIC

post-install:
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/libvdetap.so

.include <bsd.port.mk>
