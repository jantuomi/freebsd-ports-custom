PORTNAME=	taulubot
PORTVERSION=	1.0.0
PORTREVISION=	1
CATEGORIES=	net-im

MAINTAINER=	jan@jantuomi.fi
COMMENT=	Telegram bot for funny pictures of paintings haha

LICENSE=	ISCL

USE_GITHUB=	yes
GH_ACCOUNT=	jantuomi
GH_TAGNAME=	v1.0.0

NO_CHECKSUM=	yes
NO_ARCH=	yes
NO_BUILD=	yes

USES=		python:3.11+
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}aiohttp>0:www/py-aiohttp@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pillow>0:graphics/py-pillow@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}python-dotenv>0:www/py-python-dotenv@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}urllib3>0:net/py-urllib3@${PY_FLAVOR}

SUB_FILES=	pkg-message
SUB_LIST=	PYTHON_CMD=${PYTHON_CMD}

USE_RC_SUBR=	taulubot

APPDIR=		${PREFIX}/taulubot
STAGE_APPDIR=	${STAGEDIR}${APPDIR}

do-install:
	${MKDIR} ${STAGE_APPDIR}/app

	${INSTALL_DATA} ${WRKSRC}/taulubot.py ${STAGE_APPDIR}/app/
	${INSTALL_DATA} ${WRKSRC}/golden.png ${STAGE_APPDIR}/app/
	${INSTALL_DATA} ${WRKSRC}/wooden.png ${STAGE_APPDIR}/app/

	(cd ${WRKSRC}/telepot && ${COPYTREE_SHARE} . ${STAGE_APPDIR}/app/telepot)

post-install:
	@(cd ${STAGEDIR}${PREFIX} && \
		${FIND} taulubot -type f -o -type l | \
		${SORT}) >> ${TMPPLIST}

	@(cd ${STAGEDIR}${PREFIX} && \
		${FIND} taulubot -type d | \
		${SORT} -r | \
		${SED} 's|^|@dir |') >> ${TMPPLIST}

.include <bsd.port.mk>
