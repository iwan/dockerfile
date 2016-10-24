# Ruby Node on Ubuntu 16.04

This will build the base image needed to run any rails app that uses

+ Postgres Database
+ Ruby 2.3.1
+ Node JS 6.3.1

## How to Use

Very simple simply do this in your rails app

### Create Dockerfile

Create a `Dockerfile` with the following content

``` docker
FROM codemy/ruby:latest
MAINTAINER Iwan Buetti <iwan.buetti@gmail.com>

COPY . /usr/src/app

RUN bundle install --path vendor/bundle --without development test doc --deployment --jobs=4
RUN npm install && npm rebuild node-sass

RUN SECRET_KEY_BASE=blahblah AWS_ACCESS_KEY_ID=null AWS_SECRET_ACCESS_KEY=null DB_ADAPTER=nulldb bundle exec rake assets:precompile
RUN SECRET_KEY_BASE=blahblah AWS_ACCESS_KEY_ID=null AWS_SECRET_ACCESS_KEY=null DB_ADAPTER=nulldb bundle exec rake webpack:compile
```

### Build the docker image

Once you've added the docker file you can build the base image of your app using