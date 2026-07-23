PORTNAME=	pylogsentinel
PORTVERSION=	0.4.0
CATEGORIES=	sysutils
MASTER_SITES=	PYPI

MAINTAINER=	jan@jantuomi.fi
COMMENT=	Lightweight cron-friendly log monitoring utility

LICENSE=	MIT

BUILD_DEPENDS= ${PYTHON_PKGNAMEPREFIX}setuptools>=61:devel/py-setuptools@${PY_FLAVOR} \
			   ${PYTHON_PKGNAMEPREFIX}wheel>0:devel/py-wheel@${PY_FLAVOR}

USES=		python:3.11+
USE_PYTHON=	pep517 autoplist

NO_ARCH=	yes

.include <bsd.port.mk>
