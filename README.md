# README

This is a repo meant to replicate a bug in `yarn`

Getting started:

* Ruby version *2.5.1*
* Rails version *5.2.0*

* Yarn version *1.7.0*
* Node version *v10.6.0*

## To reproduce the bug:

Clone the repo:

    git clone git@github.com:kevgathuku/rails-webpacker.git

Install the ruby dependencies:

    bundle install

Install the npm dependencies by running:

    yarn

There is a `postinstall` task that should run once all the dependencies are installed.
It should run the webpack build.

Here's the full content of the `scripts` field in `package.json`:

```
"scripts": {
    "build": "npm run clean && bin/webpack",
    "clean": "rm -rf ./public/packs/*",
    "postinstall": "npm run build"
},
```

### Expected behavior:

- The `postinstall` task should be run successfully once all dependencies are installed.

### Actual behaviour:

- The `postinstall` task fails with this error message:

```
yarn install v1.7.0
[1/4] 🔍  Resolving packages...
success Already up-to-date.
$ npm run build

> rails-webpacker@ build /Users/kevin/code/ruby/rails-webpacker
> npm run clean && bin/webpack


> rails-webpacker@ clean /Users/kevin/code/ruby/rails-webpacker
> rm -rf ./public/packs/*

Could not find rake-12.3.1 in any of the sources
Run `bundle install` to install missing gems.
npm ERR! code ELIFECYCLE
npm ERR! errno 7
npm ERR! rails-webpacker@ build: `npm run clean && bin/webpack`
npm ERR! Exit status 7
npm ERR!
npm ERR! Failed at the rails-webpacker@ build script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/kevin/.npm/_logs/2018-07-12T17_02_52_269Z-debug.log
error Command failed with exit code 7.
info Visit https://yarnpkg.com/en/docs/cli/install for documentation about this command.
```

### More info

When installing the dependencies via `npm install` the `postinstall` step runs successfully.
