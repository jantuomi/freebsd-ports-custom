PORTNAME=	expense-tracker
PORTVERSION=	1.0.1
CATEGORIES=	www

MAINTAINER=	jan@jantuomi.fi
COMMENT=	Minimal personal expense tracker

LICENSE=	AGPLv3

USE_GITHUB=	yes
GH_ACCOUNT=	jantuomi
GH_PROJECT=	expense-tracker
GH_TAGNAME=	main

NO_CHECKSUM=	yes
NO_ARCH=	yes
NO_BUILD=	yes

USES=		python:3.11+
RUN_DEPENDS=	${PYTHON_CMD}:lang/python${PYTHON_SUFFIX}

SUB_LIST=	PYTHON_CMD=${PYTHON_CMD}

USE_RC_SUBR=	expense_tracker

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/expense-tracker
	${INSTALL_SCRIPT} ${WRKSRC}/app.py ${STAGEDIR}${PREFIX}/expense-tracker/
	${INSTALL_DATA} ${WRKSRC}/favicon.png ${STAGEDIR}${PREFIX}/expense-tracker/

post-install:
	@echo "expense-tracker/app.py" >> ${TMPPLIST}
	@echo "expense-tracker/favicon.png" >> ${TMPPLIST}
	@echo "@dir expense-tracker" >> ${TMPPLIST}

.include <bsd.port.mk>
