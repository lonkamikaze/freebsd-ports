# Created by: dsh@vlink.ru
# $FreeBSD$

PORTNAME=	avcheck
PORTVERSION=	0.91
CATEGORIES=	security
MASTER_SITES=	http://www.corpit.ru/ftp/avcheck/

MAINTAINER=	dsh@vlink.ru
COMMENT=	Simple antivirus solution for a mail system

MAKE_ARGS=	CC=${CC:Q} CFLAGS="${CFLAGS}"

PLIST_FILES=	man/man1/avcheck.1.gz sbin/avcheck sbin/uchroot
PORTDOCS=	README.AVP README.AVP.de README.DrWeb README.Exim \
		README.Postfix README.Postfix.de README.Sendmail eicar.msg \
		eicar.txt

OPTIONS_DEFINE=	DOCS

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/avcheck ${WRKSRC}/uchroot \
		${STAGEDIR}${PREFIX}/sbin
	${INSTALL_MAN} ${WRKSRC}/${PORTNAME}.1 ${STAGEDIR}${MANPREFIX}/man/man1

do-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S,^,${WRKSRC}/,} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
