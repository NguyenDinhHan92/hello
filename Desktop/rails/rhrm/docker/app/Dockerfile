FROM ruby:2.7.2

MAINTAINER NguyenDinhHung<nguyendinnhhung.top@gmail.com>
RUN apt-get update && apt-get install -y \
  curl \
  nano \
  build-essential \
  libpq-dev &&\
  curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
  curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
  echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
  apt-get update && apt-get install -y nodejs yarn && \
  apt-get update && apt-get install -y jpegoptim optipng pngquant

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

# Set an environment variable where the Rails app is installed to inside of Docker image
ENV RAILS_ROOT /var/www/rhrm
RUN mkdir -p $RAILS_ROOT

# Set working directory
WORKDIR $RAILS_ROOT

# Adding gems
COPY Gemfile Gemfile
COPY Gemfile.lock Gemfile.lock
RUN gem install bundler -v 2.1.4
RUN bundle install --jobs 20 --retry 5

COPY package.json .
COPY yarn.lock .
RUN yarn install --check-files

EXPOSE $RAILS_PORT
