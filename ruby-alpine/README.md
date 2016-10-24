Ruby Node on Alpine

This will build the base image needed to run any rails app that uses
+ Ruby 2.3.1
+ Node JS from Alpine Packages

## How to Use

Very simple simply do this in your rails app
 
### Create Dockerfile

Create a `Dockerfile` with the following content    

```
FROM iwan/ruby-alpine:latest
MAINTAINER Iwan Buetti <iwan.buetti@gmail.com>

COPY . /usr/src/app

RUN bundle install --path vendor/bundle --without development test doc --deployment --jobs=4
RUN SECRET_KEY_BASE=blahblah DB_ADAPTER=nulldb bundle exec rake assets:precompile
```

### Build the docker image

Once you've added the docker file you can build the base image of your app using