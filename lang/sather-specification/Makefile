# Created by: Stanislav Sedov <ssedov@mbsd.msk.ru>
# $FreeBSD$

PORTNAME=	specification
PORTVERSION=	000328
PORTREVISION=	1
CATEGORIES=	lang
MASTER_SITES=	GNU/sather/Doc
PKGNAMEPREFIX=	sather-
DISTNAME=	${PKGNAMEPREFIX}${PORTNAME}-${PORTVERSION}.html

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Specification of the Sather programming language

NO_BUILD=	yes
NO_WRKSUBDIR=	yes
DOCSDIR=	${PREFIX}/share/doc/sather/${PORTNAME}

do-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	@${TAR} -xzf ${DISTDIR}/${DISTFILES} -C ${STAGEDIR}${DOCSDIR}
	@${FIND} ${STAGEDIR}${DOCSDIR}/ -type f -exec ${CHMOD} ${SHAREMODE} {} \;

.include <bsd.port.mk>
