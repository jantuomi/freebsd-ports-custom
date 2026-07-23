PORTNAME=	pastebin
PORTVERSION=	2.0.2
CATEGORIES=	www

MAINTAINER=	jan@jantuomi.fi
COMMENT=	Minimal pastebin service
WWW=		https://github.com/w4/bin

LICENSE=	MIT

LIB_DEPENDS=	libgit2.so:devel/libgit2 \
		libonig.so:devel/oniguruma

USES=		cargo localbase

USE_GITHUB=	yes
GH_ACCOUNT=	w4
GH_PROJECT=	bin
GH_TAGNAME=	v2.0.2

NO_CHECKSUM=	yes

CARGO_INSTALL=	no

PLIST_FILES=	bin/pastebin

SUB_LIST=	PREFIX=${PREFIX}
USE_RC_SUBR=	pastebin

.sinclude "${.CURDIR}/Makefile.crates"

do-install:
	${INSTALL_PROGRAM} ${CARGO_TARGET_DIR}/release/bin ${STAGEDIR}${PREFIX}/bin/pastebin

.include <bsd.port.mk>
