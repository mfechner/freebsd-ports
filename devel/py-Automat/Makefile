# Created by: John W. O'Brien <john@saltant.com>
# $FreeBSD$

PORTNAME=	Automat
PORTVERSION=	0.5.0
CATEGORIES=	devel python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	john@saltant.com
COMMENT=	Finite-state machines in Python

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}setuptools_scm>0:devel/py-setuptools_scm \
		${PYTHON_PKGNAMEPREFIX}m2r>0:textproc/py-m2r
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}attrs>0:devel/py-attrs \
		${PYTHON_PKGNAMEPREFIX}six>0:devel/py-six

USES=		python
USE_PYTHON=	autoplist concurrent distutils

NO_ARCH=	yes

.include <bsd.port.mk>
