FROM jenkins
USER root

RUN apt-get update && apt-get dist-upgrade -fy 

# docker 
RUN apt-get -y install docker.io
RUN ln -sf /usr/bin/docker.io /usr/local/bin/docker
RUN sed -i '$acomplete -F _docker docker' /etc/bash_completion.d/docker.io
RUN update-rc.d docker.io defaults

# supervisord
RUN apt-get install -y --no-install-recommends supervisor
ADD conf/supervisor/supervisord.conf /etc/supervisor/supervisord.conf

# jenkins
USER jenkins
ENV JENKINS_HOME /var/jenkins_home
ENV JENKINS_PREFIX /

USER root
CMD ["/usr/bin/supervisord"]

EXPOSE 8080
EXPOSE 5000
