PORTNAME=	komga
DISTVERSION=	1.25.0
CATEGORIES=	www java
MASTER_SITES=	https://github.com/gotson/komga/releases/download/${DISTVERSION}/
DISTFILES=	${PORTNAME}-${DISTVERSION}.jar
EXTRACT_SUFX=	.jar
EXTRACT_ONLY=

MAINTAINER=	jan@jantuomi.fi
COMMENT=	Media server for comics, mangas, BDs, magazines, and eBooks
WWW=		https://komga.org/

LICENSE=	MIT

NO_CHECKSUM=	yes

USES=		java
JAVA_VERSION=	17+

NO_ARCH=	yes
NO_BUILD=	yes

USE_RC_SUBR=	komga
SUB_FILES=	pkg-message
SUB_LIST=	JARFILE=${JAVAJARDIR}/${PORTNAME}.jar \
		JAVA_HOME=${JAVA_HOME}

PLIST_FILES=	%%JAVAJARDIR%%/${PORTNAME}.jar

do-install:
	${MKDIR} ${STAGEDIR}${JAVAJARDIR}
	${INSTALL_DATA} ${DISTDIR}/${PORTNAME}-${DISTVERSION}.jar \
		${STAGEDIR}${JAVAJARDIR}/${PORTNAME}.jar

.include <bsd.port.mk>
