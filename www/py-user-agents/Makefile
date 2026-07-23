PORTNAME=	user-agents
PORTVERSION=	2.2.0
CATEGORIES=	www python
MASTER_SITES=	PYPI
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	jan@jantuomi.fi
COMMENT=	Library to identify devices by parsing user agent strings
WWW=		https://github.com/selwin/python-user-agents

LICENSE=	MIT

BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}setuptools>0:devel/py-setuptools@${PY_FLAVOR}
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}ua-parser>=0.10.0:www/py-ua-parser@${PY_FLAVOR}

USES=		python:3.11+
USE_PYTHON=	distutils autoplist

NO_ARCH=	yes

.include <bsd.port.mk>
