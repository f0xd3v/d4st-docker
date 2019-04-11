FROM hitko/basex-dba
MAINTAINER Eliot Kimber "ekimber@contrext.com"

# ENV HOME /opt/basex
# ENV PATH $HOME/bin:$PATH
ENV WEBAPPDIR /srv/BaseXWeb
ENV REPODIR /srv/BaseXRepo
ENV BASEX_JVM="-Dorg.basex.CHOP=false -Dorg.basex.CATFILE=/opt/dita-ot/DITA-OT/catalog-dita.xml -Dorg.basex.DTD=true -Dorg.basex.SKIPCORRUPT=true"

USER root

#
# Get the Link Manager web application source:
#
RUN mkdir -p ${REPODIR}
RUN mkdir -p ${WEBAPPDIR}/static/
RUN echo webappdir=$WEBAPPDIR

RUN wget -O /tmp/develop.zip https://github.com/dita-for-small-teams/dfst-linkmgmt-basex/archive/develop.zip
RUN unzip /tmp/develop.zip -d /tmp
RUN rm /tmp/develop.zip
RUN cp /tmp/dfst-linkmgmt-basex-develop/webapp/*.xqm ${WEBAPPDIR}/
RUN cp -r /tmp/dfst-linkmgmt-basex-develop/webapp/static/* ${WEBAPPDIR}/static/
RUN cp -r /tmp/dfst-linkmgmt-basex-develop/modules/* ${REPODIR}
RUN mkdir -p ${WEBAPPDIR}/dba/modules/modules
RUN cp /tmp/dfst-linkmgmt-basex-develop/modules/dba/*.xqm ${WEBAPPDIR}/dba/modules/
RUN cp /tmp/dfst-linkmgmt-basex-develop/modules/dba/*.xqm ${WEBAPPDIR}/dba/modules/modules/
      
COPY basex/dot_basex  /srv/.basex 
RUN chown basex /srv/.basex


# ports are defined in the basex/basexhttp base container.
# Switch to the basex user so the BaseX server will start
# correctly:
USER basex

# Specify -d to start in the background:
# ENTRYPOINT ["/opt/basex/bin/basexhttp", "-d"]

#
# End of Dockerfile
#
