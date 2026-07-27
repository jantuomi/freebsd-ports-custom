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
	(cd ${WRKSRC} && ${COPYTREE_SHARE} . ${STAGEDIR}${WWWDIR} \
		"! -name .git* ! -name Docker* ! -name docker-compose* \
		 ! -path ./.github* ! -name CHANGELOG.md ! -name README.md \
		 ! -name CONTRIBUTING.md ! -name LICENSE")
	@${MKDIR} ${STAGEDIR}/var/db/freshrss
	@${LN} -sf /var/db/freshrss ${STAGEDIR}${WWWDIR}/data
	${INSTALL_DATA} ${WRKDIR}/nginx.conf.sample \
		${STAGEDIR}${PREFIX}/etc/nginx-freshrss.conf.sample
	${INSTALL_DATA} ${FILESDIR}/php-fpm.conf.sample \
		${STAGEDIR}${PREFIX}/etc/php-fpm-freshrss.conf.sample

post-install:
	@(cd ${STAGEDIR}${WWWDIR} && \
		${FIND} . -type f -o -type l | ${SED} 's|^\./|%%WWWDIR%%/|' | \
		${SORT}) >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/nginx-freshrss.conf.sample" >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/php-fpm-freshrss.conf.sample" >> ${TMPPLIST}
	@${ECHO_CMD} "@dir(%%WWWOWN%%,%%WWWGRP%%,0750) /var/db/freshrss" >> ${TMPPLIST}

.include <bsd.port.mk>
