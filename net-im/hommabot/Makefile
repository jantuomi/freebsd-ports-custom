PORTNAME=	hommabot
PORTVERSION=	2.0.0
CATEGORIES=	net-im

MAINTAINER=	jan@jantuomi.fi
COMMENT=	Telegram bot for household task management

LICENSE=	ISCL

USE_GITHUB=	yes
GH_ACCOUNT=	jantuomi
GH_PROJECT=	hommabot2
GH_TAGNAME=	main

NO_CHECKSUM=	yes
NO_ARCH=	yes
NO_BUILD=	yes

RUN_DEPENDS=	node:www/node \
		npm:www/npm

SUB_FILES=	pkg-message
USE_RC_SUBR=	hommabot

APPDIR=		${PREFIX}/hommabot
STAGE_APPDIR=	${STAGEDIR}${APPDIR}

do-install:
	${MKDIR} ${STAGE_APPDIR}
	${INSTALL_DATA} ${WRKSRC}/package.json ${STAGE_APPDIR}/
	${INSTALL_DATA} ${WRKSRC}/package-lock.json ${STAGE_APPDIR}/
	${INSTALL_DATA} ${WRKSRC}/tsconfig.json ${STAGE_APPDIR}/
	(cd ${WRKSRC}/src && ${COPYTREE_SHARE} . ${STAGE_APPDIR}/src)

post-install:
	@(cd ${STAGEDIR}${PREFIX} && ${FIND} hommabot -type f -o -type l | ${SORT}) >> ${TMPPLIST}
	@(cd ${STAGEDIR}${PREFIX} && ${FIND} hommabot -type d | ${SORT} -r | ${SED} 's|^|@dir |') >> ${TMPPLIST}

.include <bsd.port.mk>
