# Created by: Gerrit Beine <gerrit.beine@gmx.de>
# $FreeBSD$

PORTNAME=	mastertickets
PORTVERSION=	3.0.2
PORTREVISION=	1
CATEGORIES=	www devel python
MASTER_SITES=	http://mirrors.redv.com/pub/trac/ \
		LOCAL/glarkin
PKGNAMEPREFIX=	trac-
DISTNAME=	coderanger-trac-${PORTNAME}-43a7537

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Support for ticket dependencies

RUN_DEPENDS=	trac>=0.12:www/trac

BROKEN=		unfetchable

USES=		python
USE_PYTHON=	distutils autoplist
NO_ARCH=	yes

.include <bsd.port.mk>
