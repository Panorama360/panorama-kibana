from docker.elastic.co/kibana/kibana-oss:6.2.4

USER root
RUN curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | tee /etc/yum.repos.d/yarn.repo && \
    curl --silent --location https://rpm.nodesource.com/setup_6.x | bash - && \
    yum update -y && yum install -y nodejs-6.14.0 && yum install -y yarn && yum clean all

RUN mkdir /opt/yarn_scratch && cd /opt/yarn_scratch && yarn --verbose add cytoscape qTip2 cytoscape-qtip jquery && cd /usr/share/kibana/

RUN cp -r -n /opt/yarn_scratch/node_modules/* /usr/share/kibana/node_modules && \
    rm -r /opt/yarn_scratch && \
    chown -R kibana:kibana /usr/share/kibana

USER kibana

COPY panorama-kibana-plugin.zip /opt
RUN kibana-plugin install file:///opt/panorama-kibana-plugin.zip
