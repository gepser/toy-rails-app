FROM ruby:2.5.1-slim

RUN apt-get update && apt-get install -qq -y \
    build-essential nodejs \
    libpq-dev --fix-missing --no-install-recommends apt-utils \
    libsqlite3-dev

ENV APP_PATH /usr/src/app

WORKDIR $APP_PATH
ADD Gemfile $APP_PATH
ADD Gemfile.lock $APP_PATH
RUN bundle install --jobs `expr $(cat /proc/cpuinfo | grep -c "cpu cores") - 1` --retry 3

COPY . $APP_PATH
CMD ["rails", "s"]
EXPOSE 3000
