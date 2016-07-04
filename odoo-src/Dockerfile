# Dockerfile Odoo 8 / sources

FROM alpine
MAINTAINER Leandro Augusto <leandro@zaytech.com.br>

ENV APP_VERSION 1
ENV APP RELEASE 0.1
ENV ODOO_VERSION 8.0

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh

RUN echo "# Odoo - addons OCA default " && \
    git clone -b $ODOO_VERSION https://github.com/OCA/l10n-brazil.git 		/usr/share/odoo/addons/oca-default/l10n-brazil && \
    git clone -b $ODOO_VERSION https://github.com/OCA/account-fiscal-rule.git	/usr/share/odoo/addons/oca-default/account-fiscal-rule && \
    git clone -b $ODOO_VERSION https://github.com/OCA/account-payment.git 	/usr/share/odoo/addons/oca-default/account-payment && \
    git clone -b $ODOO_VERSION https://github.com/OCA/bank-payment.git 		/usr/share/odoo/addons/oca-default/bank-payment && \
    git clone -b $ODOO_VERSION https://github.com/OCA/bank-statement-reconcile.git /usr/share/odoo/addons/oca-default/bank-statement-reconcile && \
    git clone -b $ODOO_VERSION https://github.com/OCA/bank-statement-import.git	/usr/share/odoo/addons/oca-default/bank-statement-import && \
    git clone -b $ODOO_VERSION https://github.com/OCA/sale-workflow.git 	/usr/share/odoo/addons/oca-default/sale-workflow && \
    git clone -b $ODOO_VERSION https://github.com/OCA/server-tools.git 		/usr/share/odoo/addons/oca-default/server-tools

RUN echo "# Odoo - addons OCA others " && \
    git clone -b $ODOO_VERSION https://github.com/OCA/reporting-engine.git 	/usr/share/odoo/addons/oca-others/reporting-engine && \
    git clone -b $ODOO_VERSION https://github.com/OCA/knowledge.git 		/usr/share/odoo/addons/oca-others/knowledge && \
    git clone -b $ODOO_VERSION https://github.com/OCA/margin-analysis.git 	/usr/share/odoo/addons/oca-others/margin-analysis && \
    git clone -b $ODOO_VERSION https://github.com/OCA/event.git 		/usr/share/odoo/addons/oca-others/event && \
    git clone -b $ODOO_VERSION https://github.com/OCA/department.git 		/usr/share/odoo/addons/oca-others/department && \
    git clone -b $ODOO_VERSION https://github.com/OCA/partner-contact.git 	/usr/share/odoo/addons/oca-others/partner-contact && \
    git clone -b $ODOO_VERSION https://github.com/OCA/web.git 			/usr/share/odoo/addons/oca-others/web && \
    git clone -b $ODOO_VERSION https://github.com/OCA/management-system.git 	/usr/share/odoo/addons/oca-others/management-system && \
    git clone -b $ODOO_VERSION https://github.com/OCA/commission.git 		/usr/share/odoo/addons/oca-others/commission && \
    git clone -b $ODOO_VERSION https://github.com/OCA/pos.git	 		/usr/share/odoo/addons/oca-others/pos && \
    git clone -b $ODOO_VERSION https://github.com/OCA/crm.git 			/usr/share/odoo/addons/oca-others/crm && \
    git clone -b $ODOO_VERSION https://github.com/OCA/e-commerce.git 		/usr/share/odoo/addons/oca-others/e-commerce && \
    git clone -b $ODOO_VERSION https://github.com/OCA/product-attribute.git 	/usr/share/odoo/addons/oca-others/product-attribute && \
    git clone -b $ODOO_VERSION https://github.com/OCA/website.git 		/usr/share/odoo/addons/oca-others/website && \
    git clone -b $ODOO_VERSION https://github.com/OCA/social.git 		/usr/share/odoo/addons/oca-others/social && \
    git clone -b $ODOO_VERSION https://github.com/OCA/project.git 		/usr/share/odoo/addons/oca-others/project 

RUN echo "# Odoo - addons l10n-brazil " && \ 
    git clone -b $ODOO_VERSION https://github.com/odoo-brazil/odoo-brazil-eletronic-documents.git /usr/share/odoo/addons/l10n-br/edoc && \
    git clone -b $ODOO_VERSION https://github.com/odoo-brazil/odoo-brazil-banking.git 		/usr/share/odoo/addons/l10n-br/banking && \
    git clone -b $ODOO_VERSION https://github.com/odoo-brazil/odoo-brazil-addons.git 		/usr/share/odoo/addons/l10n-br/addons && \
    git clone -b $ODOO_VERSION https://github.com/odoo-brazil/odoo-brazil-hr.git		/usr/share/odoo/addons/l10n-br/hr

RUN echo "# Odoo - addons others partners " && \
    git clone -b $ODOO_VERSION https://github.com/kmee/kmee_odoo_addons.git 		/usr/share/odoo/addons/others/kmee && \
    git clone -b $ODOO_VERSION https://github.com/Trust-Code/trust-addons.git 		/usr/share/odoo/addons/others/trust && \
    git clone -b $ODOO_VERSION https://github.com/yelizariev/addons-yelizariev.git 	/usr/share/odoo/addons/others/yelizariev && \
    git clone -b master https://github.com/ztbucardi/zaytech-odoo-addons.git    	/usr/share/odoo/addons/others/zaytech

