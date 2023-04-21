FROM debian:stretch

ENV ALIAS1="alias ll='ls -al --color=auto'"
ENV ALIAS2="alias hg='history|grep -v grep|grep -v hg|grep --color=always'"
ENV ALIAS3="alias pag='ps aux|grep -v grep|grep -v pag|grep --color=always'"
ENV ALIAS4="alias tfe='tail -f /var/log/nginx/forum-error.log|ccze -A'"
ENV ALIAS5="alias tfa='tail -f /var/log/nginx/forum-access.log|ccze -A'"
ENV ALIAS6="alias tme='tail -f /var/log/nginx/magazin-error.log|ccze -A'"
ENV ALIAS7="alias tma='tail -f /var/log/nginx/magazin-access.log|ccze -A'"

RUN apt-get update && apt-get install -y \
    nginx ccze && \
    echo "$ALIAS1" >> ~/.bashrc && \
    echo "$ALIAS2" >> ~/.bashrc && \
    echo "$ALIAS3" >> ~/.bashrc && \
    echo "$ALIAS4" >> ~/.bashrc && \
    echo "$ALIAS5" >> ~/.bashrc && \
    echo "$ALIAS6" >> ~/.bashrc && \
    echo "$ALIAS7" >> ~/.bashrc && \
    echo "source ~/.bashrc" >> ~/.bash_profile && \
    rm -rf /var/lib/apt/lists/*

ADD nginx.conf /etc/nginx/
ADD forum.conf /etc/nginx/sites-available/

RUN ln -s /etc/nginx/sites-available/forum.conf /etc/nginx/sites-enabled/forum
RUN rm /etc/nginx/sites-enabled/default

RUN echo "upstream php-upstream { server forum:9000; }" > /etc/nginx/conf.d/upstream.conf

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80
EXPOSE 443