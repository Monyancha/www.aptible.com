# ![](http://aptible-media-assets-manual.s3.amazonaws.com/web-horizontal-350.png)

[![Build Status](https://travis-ci.org/aptible/www.aptible.com.png?branch=rebrand)](https://travis-ci.org/aptible/www.aptible.com)

## www.aptible.com
Aptible's public web site is built with [Middleman](https://middlemanapp.com/).

#### Running Locally

Clone the repo:

    git clone https://github.com/aptible/www.aptible.com.git
    cd www.aptible.com/

Install necessary dependencies:

    bundle install

(Optionally) pull dynamic Resource and Blog content from Contentful:

    bundle exec rake contentful:pull

Start the server. You can access it at http://localhost:4567/

    bundle exec middleman server

If you are running [Aptible's documentation](https://github.com/aptible/docs) site
locally, set the `BASE_DOC_URL` environment variable:

    BASE_DOC_URL=http://localhost:8888 bundle exec middleman server

## Deploying

First, some prerequisites:

* [AWS CLI](http://aws.amazon.com/cli/), installed locally
* A valid `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` in your environment

In [production](https://www.aptible.com) and [staging](https://www.aptible-staging.com), the site is deployed as an S3 website (fronted by CloudFront).

To manually deploy to production, using [Omnivault](https://github.com/aptible/omnivault):

    eval $(aws-creds env default) && bundle exec rake deploy:production

Staging:

    eval $(aws-creds env default) && bundle exec rake deploy:staging

An arbitrary S3 bucket:

    eval $(aws-creds env default) && bundle exec rake deploy[bucket]

### Continuous Deployment

Travis CI deploys to both staging and production on every successful merge to
master. This requires the encrypted AWS credentials for an authorized user to
be stored in the .travis.yml configuration file.

To update these credentials at any time, run:

    travis encrypt -r aptible/www --add env AWS_ACCESS_KEY_ID=... AWS_SECRET_ACCESS_KEY=...

## Contributing

If you run into an issue that needs documentation, feel free to submit a pull
request or open an issue. We send t-shirts and swag to contributors.

## Copyright

Copyright (c) 2018 [Aptible](https://www.aptible.com). All rights reserved.
