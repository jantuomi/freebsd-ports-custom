PORTNAME=	hommabot
DISTVERSION=	2.2.0
PORTREVISION=	1
CATEGORIES=	net-im

MAINTAINER=	jan@sydanviita.fi
COMMENT=	Telegram bot for household task management
WWW=		https://github.com/jantuomi/hommabot2

LICENSE=	ISC

USE_GITHUB=	yes
GH_ACCOUNT=	jantuomi
GH_PROJECT=	hommabot2
GH_TAGNAME=	2.2.0

USES=		compiler:c++20-lang gmake python:build \
		nodejs:24,build,run \
		npm:npm,fetch,extract,build

NPM_PREFETCH=	yes
NPM_EXTRACT=	yes
NPM_REBUILD_FLAGS+=	--ignore-scripts=false --foreground-scripts --offline

USE_RC_SUBR=	hommabot
SUB_FILES=	pkg-message

APPDIR=		${PREFIX}/libexec/${PORTNAME}
STAGE_APPDIR=	${STAGEDIR}${APPDIR}

do-build:
	cd ${WRKSRC} && \
		${SETENV} ${MAKE_ENV} \
		PYTHON=${PYTHON_CMD} \
		npm_package_config_node_gyp_nodedir=${LOCALBASE} \
		npm_package_config_node_gyp_make=${MAKE_CMD} \
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
	cd ${STAGE_APPDIR} && ${SETENV} ${MAKE_ENV} ${LOCALBASE}/bin/node -e \
		'const db = new (require("better-sqlite3"))(":memory:"); db.close();'
	cd ${STAGE_APPDIR} && ${SETENV} ${MAKE_ENV} ${LOCALBASE}/bin/node -e \
		'require("esbuild").transformSync("const n: number = 1", {loader: "ts"});'
	@(cd ${STAGEDIR}${PREFIX} && \
		${FIND} libexec/${PORTNAME} \( -type f -o -type l \) | \
		${SORT}) >> ${TMPPLIST}

.include <bsd.port.mk>
