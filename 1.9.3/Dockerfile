FROM promojam/buildbox

ENV RUBY_MAJOR 1.9
ENV RUBY_VERSION 1.9.3-p547

RUN apt-get update \
        && apt-get install -y bison curl ruby procps \
        && rm -rf /var/lib/apt/lists/* \
        && mkdir -p /usr/src/ruby \
        && curl -SL "http://cache.ruby-lang.org/pub/ruby/$RUBY_MAJOR/ruby-$RUBY_VERSION.tar.bz2" \
                | tar -xjC /usr/src/ruby --strip-components=1 \
        && cd /usr/src/ruby \
        && autoconf \
        && ./configure --disable-install-doc \
        && make \
        && apt-get purge -y bison ruby procps \
        && apt-get autoremove -y \
        && make install \
        && rm -r /usr/src/ruby

RUN echo 'gem: --no-rdoc --no-ri' >> /.gemrc

RUN gem install bundler

CMD [ "irb" ]
