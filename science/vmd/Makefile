# Created by: Stephen Montgomery-Smith <stephen@math.missouri.edu>
# $FreeBSD$

PORTNAME=	vmd
DISTVERSION=	1.9.1
PORTREVISION=	4
CATEGORIES=	science graphics python tcl tk
MASTER_SITES=	http://jedi.ks.uiuc.edu/~johns/raytracer/files/0.99b2/:tachyon \
		http://www.photonlimited.com/~johns/tachyon/files/0.99b2/:tachyon \
		http://www.ks.uiuc.edu/Research/vmd/extsrcs/:stride
DISTFILES=	${VMD_DIST} \
		${TACHYON_DIST}:tachyon \
		${STRIDE_DIST}:stride

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Molecular visualization program

BUILD_DEPENDS=	makedepend:devel/makedepend \
		${PYNUMERIC}
LIB_DEPENDS=	libtcl85.so:lang/tcl85 \
		libtk85.so:x11-toolkits/tk85 \
		libfltk.so:x11-toolkits/fltk \
		libnetcdf.so:science/netcdf
RUN_DEPENDS=	${PYNUMERIC}

USES=		gmake perl5 python
USE_PERL5=	build
USE_GL=		glu
USE_GCC=	any

ONLY_FOR_ARCHS=	i386 amd64

RESTRICTED=	License has restrictions

VMD_DIST=	${PORTNAME}-${DISTVERSION}.src.tar.gz
TACHYON_DIST=	tachyon-0.99b2.tar.gz
STRIDE_DIST=	Stride_src.tar.Z

.include <bsd.port.pre.mk>

.if ${ARCH} == "amd64"
VMD_ARCH=		FREEBSDAMD64
VMD_TARGET=		freebsd.amd64.opengl
.else
VMD_ARCH=		FREEBSD
VMD_TARGET=		freebsd.opengl
.endif

PLIST_SUB+=		VMD_ARCH=${VMD_ARCH}

# Check for VMD sources
.if !exists(${DISTDIR}/${VMD_DIST})
IGNORE=	license restrictions require manual fetching of the distribution\
	source.  Please visit http://www.ks.uiuc.edu/Development/Download/download.cgi?PackageName=VMD\
	with a browser.  You will be required to register, log in,  and accept\
	the University of Illinois agreement before you can download the\
	${VMD_DIST} source file.  Place this file in ${DISTDIR} and try again.
.endif

do-extract:
	${MKDIR} ${WRKDIR}
	${TAR} -xzf ${DISTDIR}/${VMD_DIST} -C ${WRKDIR}
	${TAR} -xzf ${WRKSRC}/lib/surf/surf.tar.Z -C ${WRKSRC}/lib/surf
	${TAR} -xzf ${DISTDIR}/${TACHYON_DIST} -C ${WRKSRC}/lib
	${TAR} -xzf ${DISTDIR}/${STRIDE_DIST} -C ${WRKSRC}/lib/stride

post-patch:
	${REINPLACE_CMD} \
		-e "s|-ltk8.5|-ltk85|" \
		-e "s|-ltcl8.5|-ltcl85|" \
		-e "s%\$$python_dir/lib_\$$config_arch%${PREFIX}%" \
		-e "s|python2.5|${PYTHON_VERSION}|" \
		-e "s|%%PREFIX%%|${PREFIX}|g" \
		-e "s|/usr/local|${LOCALBASE}|g"  \
		${WRKSRC}/configure
	${REINPLACE_CMD} "s/\"gcc\"/\"${CC}\"/;s/\"g++\"/\"${CXX}\"/" \
		${WRKSRC}/configure
	${REINPLACE_CMD} -e "s/.SILENT:/#.SILENT:/" ${WRKDIR}/plugins/Makefile
	${REINPLACE_CMD} "s/.SILENT:/#.SILENT:/" ${WRKDIR}/plugins/*/Makefile
	${REINPLACE_CMD} "s%log2f(\([^ ,]*\))%logf(\1)/(float)M_LN2%g" \
		${WRKSRC}/src/Orbital.C
	${REINPLACE_CMD} -E "s/(SHLD[[:space:]]*=[[:space:]]*)gcc/\1${CC}/" \
		${WRKDIR}/plugins/Make-arch
	${REINPLACE_CMD} -E "s/(CC[[:space:]]*=[[:space:]]*)(gcc|cc)/\1${CC}/" \
		${WRKSRC}/lib/stride/Makefile \
		${WRKSRC}/lib/surf/Makefile \
		${WRKSRC}/lib/tachyon/unix/Make-arch \
		${WRKDIR}/plugins/cionize/mcudahacks/Makefile.specialbuilds \
		${WRKDIR}/plugins/cionize/Makefile.specialbuilds \
		${WRKDIR}/plugins/cionize/Makefile.mine \
		${WRKDIR}/plugins/cionize/Makefile.testing \
		${WRKDIR}/plugins/Make-arch \
		${WRKDIR}/plugins/molfile_plugin/f77/Makefile
	${REINPLACE_CMD} -E "s/(CXX[[:space:]]*=[[:space:]]*)g\+\+/\1${CXX}/" \
		${WRKDIR}/plugins/cionize/Makefile.specialbuilds \
		${WRKDIR}/plugins/fmtool/Makefile.specialbuilds \
		${WRKDIR}/plugins/hesstrans/src/foo/Makefile \
		${WRKDIR}/plugins/hesstrans/src/foo/nm_gnu.mak \
		${WRKDIR}/plugins/Make-arch

do-build:
	${SETENV} ${MAKE_ENV} ${MAKE_CMD} bsd -C ${WRKSRC}/lib/tachyon/unix \
		&& ${MV} ${WRKSRC}/lib/tachyon/compile/bsd/tachyon \
			${WRKSRC}/lib/tachyon/tachyon_${VMD_ARCH}
	${SETENV} ${MAKE_ENV} TCLLIB=-L${PREFIX}/lib/tcl8.5 \
		TCLINC=-I${PREFIX}/include/tcl8.5 PLUGINDIR=${WRKSRC}/plugins \
		${MAKE_CMD} ${VMD_ARCH} distrib -C ${WRKDIR}/plugins
	${SETENV} ${MAKE_ENV} TCL_INCLUDE_DIR=${PREFIX}/include/tcl8.5 \
		TK_INCLUDE_DIR=${PREFIX}/include/tk8.5 ${MAKE_CMD} \
		${VMD_TARGET} -C ${WRKSRC}
	${SETENV} ${MAKE_ENV} ${MAKE_CMD} all -C ${WRKSRC}/src
	${SETENV} ${MAKE_ENV} ${MAKE_CMD} depend -C ${WRKSRC}/lib/surf \
		&& ${SETENV} ${MAKE_ENV} ${MAKE_CMD} surf -C \
			${WRKSRC}/lib/surf \
		&& ${MV} ${WRKSRC}/lib/surf/surf \
			${WRKSRC}/lib/surf/surf_${VMD_ARCH}
	${SETENV} ${MAKE_ENV} ${MAKE_CMD} -C ${WRKSRC}/lib/stride \
		&& ${MV} ${WRKSRC}/lib/stride/stride \
			${WRKSRC}/lib/stride/stride_${VMD_ARCH}

do-install:
	${SETENV} ${MAKE_ENV} DESTDIR=${STAGEDIR} \
	    ${MAKE_CMD} -C ${WRKSRC}/src install
	${STRIP_CMD} ${STAGEDIR}${LOCALBASE}/lib/vmd/*${VMD_ARCH} \
	    ${STAGEDIR}${LOCALBASE}/lib/vmd/plugins/${VMD_ARCH}/molfile/*.so
.for f in tcl/autopsf1.3/psfcheck.so tcl/hesstrans1.0/hesstrans.so \
	  tcl/mutator1.4/libalchemify.so tcl/pmepot1.0/libpmepot.so \
	  tcl/psfgen1.6/libpsfgen.so tcl/rnaview1.1/rnaview \
	  tcl/signalproc1.1/specden.so tcl/signalproc1.1/fftcmds.so \
	  tcl/signalproc1.1/sgsmooth.so tcl/volutil1.3/volutil \
	  tcl/clustalw1.1/clustalw tcl/libbiokit1.1/tcl_libbiokit.so \
	  tcl/libbiokit1.1/q tcl/libbiokit1.1/seqqr \
	  tcl/libbiokit1.1/structqr tcl/libbiokit1.1/qpair \
	  tcl/libbiokit1.1/rmsd tcl/libbiokit1.1/percid \
	  tcl/phylotree1.2/upgmaclu tcl/stamp1.2/stamp \
	  bin/catdcd4.0/catdcd bin/cionize1.0/cionize
	${STRIP_CMD} ${STAGEDIR}${LOCALBASE}/lib/vmd/plugins/${VMD_ARCH}/${f}
.endfor

.include <bsd.port.post.mk>
