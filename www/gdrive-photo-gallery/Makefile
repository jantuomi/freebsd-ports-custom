PORTNAME=	gdrive-photo-gallery
PORTVERSION=	1.0.0
CATEGORIES=	www

MAINTAINER=	jan@jantuomi.fi
COMMENT=	Google Drive photo gallery web app

LICENSE=	MIT

USE_GITHUB=	yes
GH_ACCOUNT=	jantuomi
GH_PROJECT=	gdrive-photo-gallery
GH_TAGNAME=	d080e8a1e224

NO_CHECKSUM=	yes
NO_ARCH=	yes
NO_BUILD=	yes

USES=		python:3.12+
RUN_DEPENDS=	${PYTHON_CMD}:lang/python${PYTHON_SUFFIX} \
		uv:devel/uv

SUB_LIST=	PYTHON_CMD=${PYTHON_CMD}

USE_RC_SUBR=	gdrive_photo_gallery

APPDIR=		${PREFIX}/gdrive-photo-gallery
STAGE_APPDIR=	${STAGEDIR}${APPDIR}

do-install:
	${MKDIR} ${STAGE_APPDIR}
	(cd ${WRKSRC} && ${COPYTREE_SHARE} . ${STAGE_APPDIR})

post-install:
	@(cd ${STAGEDIR}${PREFIX} && \
		${FIND} gdrive-photo-gallery -type f -o -type l | \
		${SORT}) >> ${TMPPLIST}

	@(cd ${STAGEDIR}${PREFIX} && \
		${FIND} gdrive-photo-gallery -type d | \
		${SORT} -r | \
		${SED} 's|^|@dir |') >> ${TMPPLIST}

.include <bsd.port.mk>
