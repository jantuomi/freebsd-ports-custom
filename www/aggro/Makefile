PORTNAME=	aggro
PORTVERSION=	1.0.0
CATEGORIES=	www

MAINTAINER=	jan@jantuomi.fi
COMMENT=	Configurable web content aggregator with alerting

LICENSE=	MIT

USE_GITHUB=	yes
GH_ACCOUNT=	jantuomi
GH_PROJECT=	aggro
GH_TAGNAME=	main

NO_CHECKSUM=	yes
NO_ARCH=	yes
NO_BUILD=	yes

USES=		python:3.11+
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}beautifulsoup>0:www/py-beautifulsoup@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}bottle>0:www/py-bottle@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}feedparser>0:textproc/py-feedparser@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}lxml>0:devel/py-lxml@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}python-dotenv>0:www/py-python-dotenv@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}requests>0:www/py-requests@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}schedule>0:devel/py-schedule@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}sgmllib3k>0:devel/py-sgmllib3k@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}tinydb>0:databases/py-tinydb@${PY_FLAVOR}

SUB_LIST=	PYTHON_CMD=${PYTHON_CMD}

USE_RC_SUBR=	aggro

APPDIR=		${PREFIX}/aggro
STAGE_APPDIR=	${STAGEDIR}${APPDIR}

do-install:
	${MKDIR} ${STAGE_APPDIR}/app
	${MKDIR} ${STAGE_APPDIR}/plugins

	${INSTALL_DATA} ${WRKSRC}/aggro.py ${STAGE_APPDIR}/
	(cd ${WRKSRC}/app && ${COPYTREE_SHARE} . ${STAGE_APPDIR}/app)
	(cd ${WRKSRC}/plugins && ${COPYTREE_SHARE} . ${STAGE_APPDIR}/plugins)

	${INSTALL} -m 600 /dev/null ${STAGEDIR}${PREFIX}/etc/aggro.env
	${INSTALL_DATA} ${WRKSRC}/Aggrofile ${STAGEDIR}${PREFIX}/etc/Aggrofile.sample

post-install:
	@(cd ${STAGEDIR}${PREFIX} && \
		${FIND} aggro -type f -o -type l | \
		${SORT}) >> ${TMPPLIST}

	@(cd ${STAGEDIR}${PREFIX} && \
		${FIND} aggro -type d | \
		${SORT} -r | \
		${SED} 's|^|@dir |') >> ${TMPPLIST}

	@echo "etc/aggro.env" >> ${TMPPLIST}
	@echo "etc/Aggrofile.sample" >> ${TMPPLIST}

.include <bsd.port.mk>
