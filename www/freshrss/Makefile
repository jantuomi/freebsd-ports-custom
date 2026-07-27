PORTNAME=	freshrss
DISTVERSION=	1.29.1
CATEGORIES=	www
PKGNAMESUFFIX=	${PHP_PKGNAMESUFFIX}

MAINTAINER=	jan@jantuomi.fi
COMMENT=	Self-hosted RSS feed aggregator
WWW=		https://freshrss.org/

LICENSE=	AGPLv3

USES=		cpe php:web,flavors
USE_GITHUB=	yes
GH_ACCOUNT=	FreshRSS
GH_PROJECT=	FreshRSS

NO_CHECKSUM=	yes

USE_PHP=	ctype curl dom filter gd iconv mbstring pdo pdo_sqlite \
		phar posix session simplexml sqlite3 tokenizer xml \
		xmlreader xmlwriter zip

NO_ARCH=	yes
NO_BUILD=	yes

PLIST_SUB=	WWWGRP=${WWWGRP} \
		WWWOWN=${WWWOWN}

SUB_FILES=	pkg-message nginx.conf.sample
SUB_LIST=	WWWDIR=${WWWDIR}

do-install:
	@${MKDIR} ${STAGEDIR}${WWWDIR}
	(cd ${WRKSRC} && ${COPYTREE_SHARE} app ${STAGEDIR}${WWWDIR})
	(cd ${WRKSRC} && ${COPYTREE_SHARE} cli ${STAGEDIR}${WWWDIR})
	(cd ${WRKSRC} && ${COPYTREE_SHARE} extensions ${STAGEDIR}${WWWDIR})
	(cd ${WRKSRC} && ${COPYTREE_SHARE} lib ${STAGEDIR}${WWWDIR})
	(cd ${WRKSRC} && ${COPYTREE_SHARE} p ${STAGEDIR}${WWWDIR})
	${INSTALL_DATA} ${WRKSRC}/config.default.php ${STAGEDIR}${WWWDIR}/
	${INSTALL_DATA} ${WRKSRC}/config-user.default.php ${STAGEDIR}${WWWDIR}/
	${INSTALL_DATA} ${WRKSRC}/constants.php ${STAGEDIR}${WWWDIR}/
	${INSTALL_DATA} ${WRKSRC}/index.html ${STAGEDIR}${WWWDIR}/
	${INSTALL_DATA} ${WRKSRC}/index.php ${STAGEDIR}${WWWDIR}/
	${INSTALL_DATA} ${WRKSRC}/force-https.default.txt ${STAGEDIR}${WWWDIR}/
	${INSTALL_DATA} ${WRKSRC}/opml.default.xml ${STAGEDIR}${WWWDIR}/
	@${MKDIR} ${STAGEDIR}/var/db/freshrss
	@${LN} -sf /var/db/freshrss ${STAGEDIR}${WWWDIR}/data
	${INSTALL_DATA} ${WRKDIR}/nginx.conf.sample \
		${STAGEDIR}${PREFIX}/etc/nginx-freshrss.conf.sample
	${INSTALL_DATA} ${FILESDIR}/php-fpm.conf.sample \
		${STAGEDIR}${PREFIX}/etc/php-fpm-freshrss.conf.sample

post-install:
	@(cd ${STAGEDIR}${WWWDIR} && \
		${FIND} . -type f -o -type l | ${SED} 's|^\./|${WWWDIR_REL}/|' | \
		${SORT}) >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/nginx-freshrss.conf.sample" >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/php-fpm-freshrss.conf.sample" >> ${TMPPLIST}
	@${ECHO_CMD} "@dir(${WWWOWN},${WWWGRP},0750) /var/db/freshrss" >> ${TMPPLIST}

.include <bsd.port.mk>
