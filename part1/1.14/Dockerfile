FROM ruby:2.6.0

WORKDIR /app

RUN apt-get update && apt-get install -y git nodejs

RUN gem install bundler

RUN git clone https://github.com/docker-hy/rails-example-project

WORKDIR /app/rails-example-project

RUN bundle install

RUN rails db:migrate

EXPOSE 3000

CMD ["rails", "s"]
