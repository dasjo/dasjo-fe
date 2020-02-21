# dasjo-fe

## Requirements

* yarn https://yarnpkg.com/en/docs/install
* gridsome https://gridsome.org/docs/#prerequisites

## Setup

* Make sure https://github.com/dasjo/dasjo-be is running and available on http://dasjo-be.docksal/jsonapi
* git clone git@github.com:dasjo/dasjo-fe.git
* cd dasjo-fe

## Usage

* gridsome develop
* gridsome build

# Drupal starter for Gridsome

## Install
> NOTE: this cli command isn't available yet

`gridsome create my-gridsome-project drupal`

## Guide

### With `.env`
Add your Drupal API Base URL to a .env file:

`APP_BASE_URL=https://somedrupalsite.pantheon.io`

```js
// gridsome.config.js

require('dotenv').config()
const { defaultExcludes } = require('@gridsome/source-drupal')

module.exports = {
  chainWebpack: config => {
    config
      .plugin('env')
      .use(require.resolve('webpack/lib/EnvironmentPlugin'), ['APP_BASE_URL'])
  },
  siteName: 'Gridsome',
  siteDescription: 'A Drupal starter for Gridsome',
  plugins: [
    {
      use: '@gridsome/source-drupal',
      options: {
        baseUrl: process.env.APP_BASE_URL, // use dotenv with .env or replace value with your Drupal url
        exclude: [ ...defaultExcludes /* include your own excludes here */],
        routes: {
          'node--article': '/articles/:title',
          'taxonomy_term--tags': '/tags/:title'
        }
      }
    }
  ]
}

```

### Without `.env`
Replace `baseUrl` with your Drupal API URL.

```js
// gridsome.config.js

const { defaultExcludes } = require('@gridsome/source-drupal')

module.exports = {
  siteName: 'Gridsome',
  siteDescription: 'A Drupal starter for Gridsome',
  plugins: [
    {
      use: '@gridsome/source-drupal',
      options: {
        baseUrl: 'https://somedrupalsite.pantheon.io',
        exclude: [ ...defaultExcludes /* include your own excludes here */],
        routes: {
          'node--article': '/articles/:title',
          'taxonomy_term--tags': '/tags/:title'
        }
      }
    }
  ]
}

```

### Contenta CMS
Replace `baseUrl` with your Contenta CMS API URL.

```js
// gridsome.config.js

const { defaultExcludes } = require('@gridsome/source-drupal')

module.exports = {
  siteName: 'Gridsome',
  siteDescription: 'A Drupal (Contenta CMS) starter for Gridsome',
  plugins: [
    {
      use: '@gridsome/source-drupal',
      options: {
        baseUrl: 'https://live-contentacms.pantheonsite.io',
        apiBase: 'api',
        exclude: [ ...defaultExcludes ],
        routes: {
          'article': '/articles/:title',
          'recipes': '/recipes/:title'
        }
      }
    }
  ]
}

```

## Included templates

This starter includes basic templates for Drupal Aritcles, Basic Pages and tags.
