> :warning: Latest Amber `v0.7.2` is not compatible with Crystal `v0.25.0`

> Please use a `.crystal-version` file with `0.24.2` instead

# Amber Heroku Buildpack

> Based on [Crystal Heroku Buildpack](https://github.com/crystal-lang/heroku-buildpack-crystal)

[![Amber logo](https://i.imgur.com/NEodgHV.png)](https://amberframework.org)

You can create an app in Heroku with Amber's buildpack by running the
following command:

```bash
$ heroku create myapp --buildpack amberframework/amber
```

The default behaviour is to use the [latest crystal release](https://github.com/crystal-lang/crystal/releases/latest).
If you need to use a specific version create a `.crystal-version` file in your
application root directory with the version that should be used (e.g. `0.17.1`).

## Requirements

In order for the buildpack to work properly you should have a `shard.yml` file,
as it is how it will detect that your app is a Crystal app.

Your application has to listen on a port defined by Heroku.

Append the following code to your `config/application.cr` file:

```crystal
Amber::Server.configure do |settings|
  settings.port = ENV["PORT"].to_i if ENV["PORT"]?
end
```

To be able to use production enviroment config Heroku needs `.amber_secret_key` or `.encryption_key` during compilation process, so in this case you should remove the encryption key from `.gitignore` file.

> DISCLAIMER: Don't publish encryption key in open source projects if you have sensitive config

## Testing

To test a change to this buildpack, write a unit test in `tests/run` that asserts your change and
run `make test` to ensure the change works as intended and does not break backwards compatibility.

## More info

This buildpack have been configured to work with [Amber Framework](https://amberframework.org/) projects.

To learn more about how to deploy other Crystal applications to Heroku, read
[this blog post](http://crystal-lang.org/2016/05/26/heroku-buildpack.html).

## Older versions of Crystal

Currently latest Amber `v0.3.6` is compatible with Crystal `v0.23.1`

Other versions aren't guaranteed to be compatible.

## Edge version of the buildpack

The `amberframework/amber` buildpack from the [Heroku Registry](https://devcenter.heroku.com/articles/buildpack-registry) contains the latest stable version of the buildpack. If you'd like to use the latest buildpack code from this Github repository, you can set your buildpack to the Github URL:

    heroku buildpacks:set https://github.com/amberframework/heroku-buildpack-amber
 
