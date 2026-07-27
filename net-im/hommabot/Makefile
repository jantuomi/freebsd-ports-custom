PORTNAME=	hommabot
DISTVERSION=	2.1.0
PORTREVISION=	2
CATEGORIES=	net-im

MAINTAINER=	jan@jantuomi.fi
COMMENT=	Telegram bot for household task management
WWW=		https://github.com/jantuomi/hommabot2

LICENSE=	ISC

USE_GITHUB=	yes
GH_ACCOUNT=	jantuomi
GH_PROJECT=	hommabot2
GH_TAGNAME=	f7e272ab8726ed6a205b46d6723cc91aa9d63be1

USES=		python:build \
		nodejs:24,build,run \
		npm:npm,fetch,extract,build

NPM_PREFETCH=	yes
NPM_EXTRACT=	yes

USE_RC_SUBR=	hommabot
SUB_FILES=	pkg-message

APPDIR=		${PREFIX}/libexec/${PORTNAME}
STAGE_APPDIR=	${STAGEDIR}${APPDIR}

do-build:
	cd ${WRKSRC} && \
		${SETENV} ${MAKE_ENV} \
		npm_config_python=${PYTHON_CMD} \
		npm_config_nodedir=${LOCALBASE} \
		npm_config_build_from_source=true \
		${NPM_REBUILD_CMD} ${NPM_REBUILD_FLAGS}

do-install:
	${MKDIR} ${STAGE_APPDIR}
	${INSTALL_DATA} ${WRKSRC}/package.json \
		${STAGE_APPDIR}/
	${INSTALL_DATA} ${WRKSRC}/package-lock.json \
		${STAGE_APPDIR}/
	${INSTALL_DATA} ${WRKSRC}/tsconfig.json \
		${STAGE_APPDIR}/
	(cd ${WRKSRC} && \
		${COPYTREE_SHARE} src ${STAGE_APPDIR})
	cd ${WRKSRC} && ${TAR} -cf - node_modules | ${TAR} -xf - -C ${STAGE_APPDIR}

post-install:
	@(cd ${STAGEDIR}${PREFIX} && \
		${FIND} libexec/${PORTNAME} \( -type f -o -type l \) | \
		${SORT}) >> ${TMPPLIST}

.include <bsd.port.mk>
