FROM ruby
RUN apt-get update -y && apt-get install -y build-essential libpq-dev nodejs sqlite3 ruby-full
RUN gem install bundler

ONBUILD COPY app /usr/src
ONBUILD WORKDIR /usr/src/app

ONBUILD EXPOSE 3000
ONBUILD RUN bundle install
ONBUILD RUN rake db:migrate
ONBUILD RUN rake db:seed

# docker build -t ft-rails:on-build .
