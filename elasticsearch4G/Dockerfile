FROM elasticsearch:7.11.1
LABEL author="sorabh86"
LABEL author_email="ssorabh.ssharma@hotmail.com"

RUN sed -i 's/## -Xms4g/-Xms4g/' /usr/share/elasticsearch/config/jvm.options

RUN sed -i 's/## -Xmx4g/-Xmx4g/' /usr/share/elasticsearch/config/jvm.options
