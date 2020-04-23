FROM ruby:2.5.7

RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -

RUN apt-get update -qq && apt-get install -y \
  build-essential \
  nodejs \
  git-flow \
  yarn \
  vim

ENV EDITOR=vim

RUN ln -sf /usr/bin/nodejs /usr/local/bin/node

ENV BUNDLE_PATH=/bundle
ENV BUNDLE_BIN=/bundle/bin
ENV GEM_HOME=/bundle
ENV PATH="${BUNDLE_BIN}:${PATH}"

EXPOSE 4567
EXPOSE 35730

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN groupadd -g 1000 app
RUN groupadd -g 999 docker
RUN useradd -m -u 1000 -g 999 -s /bin/bash app

COPY . ./

COPY entrypoint.sh /usr/bin
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

USER app
CMD ["bash"]