PORTNAME=	diddle
PORTVERSION=	1.0.0
PORTREVISION=	1
CATEGORIES=	www

MAINTAINER=	jan@jantuomi.fi
COMMENT=	Minimalist self-hosted Doodle alternative

LICENSE=	APACHE20

USE_GITHUB=	yes
GH_ACCOUNT=	jantuomi
GH_PROJECT=	diddle
GH_TAGNAME=	main

NO_CHECKSUM=	yes
NO_ARCH=	yes
NO_BUILD=	yes

USES=		python:3.11+
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}flask>0:www/py-flask@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}Flask-Compress>0:www/py-flask-compress@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}gunicorn>0:www/py-gunicorn@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}python-dotenv>0:www/py-python-dotenv@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pyyaml>0:devel/py-pyyaml@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}sqlite3>0:databases/py-sqlite3@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}ua-parser>0:www/py-ua-parser@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}user-agents>0:www/py-user-agents@${PY_FLAVOR}

SUB_FILES=	pkg-message
SUB_LIST=	PYTHON_CMD=${PYTHON_CMD}

USE_RC_SUBR=	diddle

APPDIR=		${PREFIX}/diddle
STAGE_APPDIR=	${STAGEDIR}${APPDIR}

do-install:
	${MKDIR} ${STAGE_APPDIR}/app

	${INSTALL_DATA} ${WRKSRC}/app.py ${STAGE_APPDIR}/app/
	${INSTALL_DATA} ${WRKSRC}/db.py ${STAGE_APPDIR}/app/
	${INSTALL_DATA} ${WRKSRC}/email_client.py ${STAGE_APPDIR}/app/
	${INSTALL_DATA} ${WRKSRC}/apply_migrations.py ${STAGE_APPDIR}/app/

	(cd ${WRKSRC}/migrations && ${COPYTREE_SHARE} . ${STAGE_APPDIR}/app/migrations)
	(cd ${WRKSRC}/static && ${COPYTREE_SHARE} . ${STAGE_APPDIR}/app/static)
	(cd ${WRKSRC}/templates && ${COPYTREE_SHARE} . ${STAGE_APPDIR}/app/templates)

post-install:
	@(cd ${STAGEDIR}${PREFIX} && \
		${FIND} diddle -type f -o -type l | \
		${SORT}) >> ${TMPPLIST}

	@(cd ${STAGEDIR}${PREFIX} && \
		${FIND} diddle -type d | \
		${SORT} -r | \
		${SED} 's|^|@dir |') >> ${TMPPLIST}

.include <bsd.port.mk>
