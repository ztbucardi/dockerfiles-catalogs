# Dockerfile Odoo 8 / l10n_br - server base

FROM ubuntu:14.04
MAINTAINER Leandro Augusto <leandro@zaytech.com.br>

ENV ODOO_VERSION 1
ENV ODOO_RELEASE 0.1
ENV DEBIAN_FRONTEND noninteractive


# Install pacotes basicos

ADD files/apt-requirements /tmp/apt-requirements
RUN apt-get -qq update \
    && apt-get -qq dist-upgrade \
    && apt-get install -y -q $(grep -v '^#' /tmp/apt-requirements)


# Install e configura localizacao

RUN locale-gen pt_BR.UTF-8 \
    && update-locale LANG=pt_BR.UTF-8 \
    && ln -sf /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime \
    && echo "America/Sao_Paulo" > /etc/timezone \
    && dpkg-reconfigure -f noninteractive tzdata


# Estrutura paths

WORKDIR /opt/odoo/

RUN bash -c \
    'mkdir -p /opt/odoo/{etc,lib,log,var,tmp,server,addons} \
     && mkdir -p /opt/odoo/var/{dados,xml} \
     && mkdir -p /opt/odoo/var/xml/{bkp,exp,imp}'

RUN ln -s /opt/odoo/etc/ /etc/odoo \
    && ln -s /opt/odoo/log/ /var/log/odoo \
    && ln -sf /opt/odoo/server/OCB/openerp-server /usr/bin/odoo-server

ADD files/confs/odoo.conf /opt/odoo/etc/odoo.conf
RUN touch /var/log/odoo/odoo.log \
    && touch /var/run/odoo.pid

RUN groupadd --gid 501 odoo \
    && useradd --system --uid 501 --gid 501 --home /opt --shell /bin/bash odoo \
    && chown -R odoo:odoo /opt/odoo \
    && chown -R odoo:odoo /etc/odoo/odoo.conf \
    && chown -R odoo:odoo /var/log/odoo \
    && chown odoo:odoo /var/run/odoo.pid


# Install requirements & libs

ADD files/pip-requirements /tmp/pip-requirements
ADD http://download.gna.org/wkhtmltopdf/0.12/0.12.1/wkhtmltox-0.12.1_linux-trusty-amd64.deb /tmp/wkhtmltox.deb
RUN pip install -r /tmp/pip-requirements && \
    dpkg -i /tmp/wkhtmltox.deb


RUN mkdir /tmp/.python-eggs && chown -R odoo /tmp/.python-eggs
ENV PYTHON_EGG_CACHE /tmp/.python-eggs

WORKDIR /opt/odoo/lib/
RUN git clone https://github.com/odoo-brazil/PySPED.git --branch 8.0 && \
    git clone https://github.com/odoo-brazil/pyxmlsec --branch master

RUN cd /opt/odoo/lib/PySPED ; python setup.py install && \
    cd /opt/odoo/libpyxmlsec ; python setup.py install


# Install supervisor
RUN apt-get install -y -qq supervisor
ADD files/confs/supervisord.conf /etc/supervisor/supervisord.conf


# Limpando o ambiente
WORKDIR /opt/odoo
RUN apt-get autoremove -y && \
    apt-get autoclean


CMD ["/usr/bin/supervisord"]
