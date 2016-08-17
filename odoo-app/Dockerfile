# Dockerfile Odoo 8 / l10n_br - server base

FROM ubuntu:14.04
MAINTAINER Leandro Augusto <leandro@zaytech.com.br>

ENV ODOO_VERSION 8.0
ENV APP_VERSION 1
ENV APP_RELEASE 0.7

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
    'mkdir -p /opt/odoo \
    && mkdir -p /var/log/odoo'

RUN touch /var/log/odoo/odoo.log \
    && touch /var/run/odoo.pid
RUN adduser --disabled-password --gecos '' r && adduser r sudo && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

RUN groupadd --gid 501 odoo \
    && useradd --system --uid 501 --gid 501 --home /opt/odoo --shell /bin/bash odoo \
    && usermod -a -G sudo odoo \
    && chown -R odoo:odoo /opt/odoo \
    && chown -R odoo:odoo /var/log/odoo \
    && chown odoo:odoo /var/run/odoo.pid \
    && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers


# Install requirements for website build themes

RUN apt-get install -y npm \
    ln -s /usr/bin/nodejs /usr/bin/node \
    npm install -g less less-plugin-clean-css


# Install requirements & libs

WORKDIR /tmp/

ADD files/pip-requirements /tmp/pip-requirements
ADD https://raw.githubusercontent.com/OCA/OCB/8.0/requirements.txt /tmp/pip-requirements-ocb

ADD http://download.gna.org/wkhtmltopdf/0.12/0.12.1/wkhtmltox-0.12.1_linux-trusty-amd64.deb /tmp/wkhtmltox.deb

RUN pip install -r /tmp/pip-requirements && \
    pip install -r /tmp/pip-requirements-ocb && \
    dpkg -i /tmp/wkhtmltox.deb

RUN mkdir /tmp/.python-eggs && chown -R odoo /tmp/.python-eggs
ENV PYTHON_EGG_CACHE /tmp/.python-eggs
RUN git clone https://github.com/odoo-brazil/PySPED.git --branch 8.0 && \
    git clone https://github.com/odoo-brazil/pyxmlsec --branch master

RUN cd /tmp/PySPED ; python setup.py install && \
    cd /tmp/libpyxmlsec ; python setup.py install


# Limpando o ambiente
RUN apt-get autoremove -y && \
    apt-get autoclean

USER odoo
CMD ["python", "/opt/odoo/server/OCB/odoo.py", "--config=/opt/odoo/odoo.conf"]
