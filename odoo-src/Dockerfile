# Dockerfile Odoo 8 / sources

FROM alpine
MAINTAINER Leandro Augusto <leandro@zaytech.com.br>

ENV APP_VERSION 1
ENV APP RELEASE 0.1

ENV ODOO_VERSION 8.0
ENV ODOO_PATH /opt/odoo
ENV GIT_CMD "git clone --depth 1 "

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh

RUN echo "# Odoo - server OCA " && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/OCB.git			$ODOO_PATH/server/OCB

RUN echo "# Odoo - addons OCA default " && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/l10n-brazil.git 		$ODOO_PATH/addons/oca-default/l10n-brazil && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/account-fiscal-rule.git	$ODOO_PATH/addons/oca-default/account-fiscal-rule && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/account-payment.git 	$ODOO_PATH/addons/oca-default/account-payment && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/bank-payment.git 		$ODOO_PATH/addons/oca-default/bank-payment && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/bank-statement-reconcile.git 	$ODOO_PATH/addons/oca-default/bank-statement-reconcile && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/bank-statement-import.git		$ODOO_PATH/addons/oca-default/bank-statement-import && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/sale-workflow.git 			$ODOO_PATH/addons/oca-default/sale-workflow && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/server-tools.git 			$ODOO_PATH/addons/oca-default/server-tools

RUN echo "# Odoo - addons OCA others " && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/reporting-engine.git 	$ODOO_PATH/addons/oca-others/reporting-engine && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/knowledge.git 		$ODOO_PATH/addons/oca-others/knowledge && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/margin-analysis.git 	$ODOO_PATH/addons/oca-others/margin-analysis && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/event.git 		$ODOO_PATH/addons/oca-others/event && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/department.git 		$ODOO_PATH/addons/oca-others/department && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/partner-contact.git 	$ODOO_PATH/addons/oca-others/partner-contact && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/web.git 			$ODOO_PATH/addons/oca-others/web && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/management-system.git 	$ODOO_PATH/addons/oca-others/management-system && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/commission.git 		$ODOO_PATH/addons/oca-others/commission && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/pos.git	 		$ODOO_PATH/addons/oca-others/pos && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/crm.git 			$ODOO_PATH/addons/oca-others/crm && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/e-commerce.git 		$ODOO_PATH/addons/oca-others/e-commerce && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/product-attribute.git 	$ODOO_PATH/addons/oca-others/product-attribute && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/website.git 		$ODOO_PATH/addons/oca-others/website && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/social.git 		$ODOO_PATH/addons/oca-others/social && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/OCA/project.git 		$ODOO_PATH/addons/oca-others/project 

RUN echo "# Odoo - addons l10n-brazil " && \ 
    $GIT_CMD -b $ODOO_VERSION https://github.com/odoo-brazil/odoo-brazil-eletronic-documents.git 	$ODOO_PATH/addons/l10n-br/edoc && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/odoo-brazil/odoo-brazil-banking.git 			$ODOO_PATH/addons/l10n-br/banking && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/odoo-brazil/odoo-brazil-addons.git 			$ODOO_PATH/addons/l10n-br/addons && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/odoo-brazil/odoo-brazil-hr.git				$ODOO_PATH/addons/l10n-br/hr

RUN echo "# Odoo - addons others partners " && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/kmee/kmee_odoo_addons.git 		$ODOO_PATH/addons/others/kmee && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/Trust-Code/trust-addons.git 		$ODOO_PATH/addons/others/trust && \
    $GIT_CMD -b $ODOO_VERSION https://github.com/yelizariev/addons-yelizariev.git 	$ODOO_PATH/addons/others/yelizariev && \
    $GIT_CMD -b master https://github.com/ztbucardi/zaytech-odoo-addons.git    		$ODOO_PATH/addons/others/zaytech


VOLUME ["/opt/odoo/server","/opt/odoo/addons"]
