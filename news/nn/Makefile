# Created by: adam
# $FreeBSD$

PORTNAME=	nn
PORTVERSION=	6.7.3
PORTREVISION=	1
CATEGORIES=	news
MASTER_SITES=	http://www.sourcefiles.org/Internet/News/Usenet_Clients/  \
		http://www.wa.apana.org.au/~dean/sources/

MAINTAINER=	johans@FreeBSD.org
COMMENT=	Newsreader

USES=		tar:Z
MAKE_ARGS=	CC=${CC:Q} CFLAGS="${CFLAGS} -Iconf" LDFLAGS="${LDFLAGS} -s"

pre-patch:
	@${CP} ${WRKSRC}/config.h-dist ${WRKSRC}/config.h.unparsed

pre-build:
	@${SED} 's#SUB_PREFIX#${PREFIX}#; s#SUB_MANPREFIX#${MANPREFIX}#' \
		${WRKSRC}/config.h.unparsed > ${WRKSRC}/config.h

post-build:
	@${REINPLACE_CMD} 's#${PREFIX}#$${DESTDIR}&#' ${WRKSRC}/inst

.include <bsd.port.mk>
