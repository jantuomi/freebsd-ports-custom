PORTNAME=	thelounge
DISTVERSION=	4.5.2
CATEGORIES=	net-im

MAINTAINER=	jan@jantuomi.fi
COMMENT=	Modern, responsive, cross-platform, self-hosted IRC client
WWW=		https://thelounge.chat/

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

USE_GITHUB=	yes
GH_ACCOUNT=	thelounge
GH_PROJECT=	thelounge
GH_TAGNAME=	v${DISTVERSION}

NO_CHECKSUM=	yes

USES=		nodejs:24,build,run \
		npm:yarn1,fetch,extract,build

NPM_PREFETCH=	yes
NPM_EXTRACT=	yes

USE_RC_SUBR=	thelounge
SUB_FILES=	pkg-message

APPDIR=		${PREFIX}/libexec/${PORTNAME}
STAGE_APPDIR=	${STAGEDIR}${APPDIR}

do-build:
	cd ${WRKSRC} && \
		${SETENV} ${MAKE_ENV} NODE_ENV=production \
		${NPM_EXEC_CMD} ${NPM_EXEC_FLAGS} -- run-p --aggregate-output build:client build:server

do-install:
	${MKDIR} ${STAGE_APPDIR}
	${INSTALL_DATA} ${WRKSRC}/package.json ${STAGE_APPDIR}/
	${INSTALL_DATA} ${WRKSRC}/index.js ${STAGE_APPDIR}/
	(cd ${WRKSRC} && ${COPYTREE_SHARE} dist ${STAGE_APPDIR})
	(cd ${WRKSRC} && ${COPYTREE_SHARE} public ${STAGE_APPDIR})
	(cd ${WRKSRC} && ${COPYTREE_SHARE} defaults ${STAGE_APPDIR})
	cd ${WRKSRC} && ${TAR} -cf - node_modules | ${TAR} -xf - -C ${STAGE_APPDIR}
	${LN} -sf ${APPDIR}/index.js ${STAGEDIR}${PREFIX}/bin/thelounge
	${MKDIR} ${STAGEDIR}/var/db/thelounge
	${INSTALL_DATA} ${FILESDIR}/config.js.sample \
		${STAGEDIR}${PREFIX}/etc/thelounge.conf.sample

post-install:
	@(cd ${STAGEDIR}${PREFIX} && \
		${FIND} libexec/${PORTNAME} \( -type f -o -type l \) | \
		${SORT}) >> ${TMPPLIST}

.include <bsd.port.mk>
