# Screwdriver API
[![Version][npm-image]][npm-url] [![Pulls][docker-pulls]][docker-url] [![Stars][docker-stars]][docker-url] [![Build Status][status-image]][status-url] [![Open Issues][issues-image]][issues-url] [![Dependency Status][daviddm-image]][daviddm-url] [![Coverage][cov-image]][cov-url] [![Vulnerabilities][vul-image]][vul-url] ![License][license-image] [![Slack][slack-image]][slack-url]

> API for the Screwdriver CD service

## Usage

### Prerequisites

- Node v6.0.0 or higher

### From Source

```bash
$ git clone git@github.com:screwdriver-cd/screwdriver.git ./
$ npm install
$ vim ./config/local.yaml # See below for configuration
$ npm start
info: Server running at http://localhost:8080
```

### Prebuilt Docker image

```bash
$ vim ./local.yaml # See below for configuration
$ docker run --rm -it --volume=`pwd`/local.yaml:/config/local.yaml -p 8080 screwdrivercd/screwdriver:stable
info: Server running at http://localhost:8080
```

### In-A-Box

This handy feature will bring up an entire Screwdriver instance (ui, api, and log store) locally for you to play with.
All data written to a database will be stored in `data` directory.

Requires:
 - Mac OSX 10.10+
 - [Docker for Mac][docker]
 - [Docker Compose 1.8.1+][docker-compose]

```bash
$ python <(curl https://raw.githubusercontent.com/screwdriver-cd/screwdriver/master/in-a-box.py)
```

## Configuration

Screwdriver already [defaults most configuration](config/default.yaml), but you can override defaults using a `local.yaml` or environment variables.

### Yaml

Example overriding `local.yaml`:

```yaml
executor:
    plugin: k8s
    k8s:
        host: 127.0.0.1
        token: this-is-a-real-token

login:
    oauthClientId: totally-real-client-id
    oauthClientSecret: another-real-client-secret
```

### Environment

Example overriding with environment variables:

```bash
$ export K8S_HOST=127.0.0.1
$ export K8S_TOKEN=this-is-a-real-token
$ export SECRET_OAUTH_CLIENT_ID=totally-real-client-id
$ export SECRET_OAUTH_CLIENT_SECRET=another-real-client-secret
```

All the possible environment variables are [defined here](config/custom-environment-variables.yaml).

## Plugins

This API comes preloaded with 7 (seven) resources:

 - [auth](plugins/auth/README.md)
 - [builds](plugins/builds/README.md)
 - [events](plugins/events/README.md)
 - [jobs](plugins/jobs/README.md)
 - [pipelines](plugins/pipelines/README.md)
 - [secrets](plugins/secrets/README.md)
 - [webhooks](plugins/webhooks/README.md)

One (1) option for datastores:
 - Postgres, MySQL, and Sqlite (`sequelize`)

Two (2) options for executor:
 - Kubernetes (`k8s`)
 - Docker (`docker`)

Two (2) options for SCM:
 - Github (`github`)
 - Bitbucket (`bitbucket`)

## Testing

### Unit Tests

```bash
npm test
```

### Functional tests

Fork `functional-*` repositories to your organization from [screwdriver-cd-test](https://github.com/screwdriver-cd-test)

Update `.func_config.json` with your own username, github token, access key, host, and organization for test:
```json
{
    "username": "YOUR-GITHUB-USERNAME",
    "gitToken": "YOUR-ACCESS-TOKEN",
    "accessKey": "YOUR-ACCESS-KEY",
    "host": "YOUR-LOCAL-API-HOST",
    "testOrg": "YOUR-TEST-ORGANIZATION"
}
```

Then run the cucumber tests:
```bash
npm run functional
```

## License

Code licensed under the BSD 3-Clause license. See LICENSE file for terms.

[npm-image]: https://img.shields.io/npm/v/screwdriver-api.svg
[npm-url]: https://npmjs.org/package/screwdriver-api
[cov-image]: https://coveralls.io/repos/github/screwdriver-cd/screwdriver/badge.svg?branch=master
[cov-url]: https://coveralls.io/github/screwdriver-cd/screwdriver?branch=master
[vul-image]: https://snyk.io/test/github/screwdriver-cd/screwdriver.git/badge.svg
[vul-url]: https://snyk.io/test/github/screwdriver-cd/screwdriver.git
[docker-pulls]: https://img.shields.io/docker/pulls/screwdrivercd/screwdriver.svg
[docker-stars]: https://img.shields.io/docker/stars/screwdrivercd/screwdriver.svg
[docker-url]: https://hub.docker.com/r/screwdrivercd/screwdriver/
[license-image]: https://img.shields.io/npm/l/screwdriver-api.svg
[issues-image]: https://img.shields.io/github/issues/screwdriver-cd/screwdriver.svg
[issues-url]: https://github.com/screwdriver-cd/screwdriver/issues
[status-image]: https://cd.screwdriver.cd/pipelines/1/badge
[status-url]: https://cd.screwdriver.cd/pipelines/1
[daviddm-image]: https://david-dm.org/screwdriver-cd/screwdriver.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/screwdriver-cd/screwdriver
[slack-image]: http://slack.screwdriver.cd/badge.svg
[slack-url]: http://slack.screwdriver.cd/
[docker-compose]: https://www.docker.com/products/docker-compose
[docker]: https://www.docker.com/products/docker
