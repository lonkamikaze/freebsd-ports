# $FreeBSD$

PORTNAME=	zmq
PORTVERSION=	1.1.3
PORTREVISION=	1
CATEGORIES=	net pear
MASTER_SITES=	http://pecl.php.net/get/
PKGNAMEPREFIX=	pecl-
DIST_SUBDIR=	PECL

MAINTAINER=	garga@FreeBSD.org
COMMENT=	PHP bindings for ZeroMQ

LICENSE=	BSD3CLAUSE

LIB_DEPENDS=	libzmq.so:net/libzmq4

USES=		tar:tgz pkgconfig
USE_PHP=	yes
USE_PHPIZE=	yes
USE_PHPEXT=	yes

.include <bsd.port.mk>
