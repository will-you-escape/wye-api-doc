
Introduction
------------
This documentation has been generated with [Slate](https://github.com/lord/slate)

### Local development prerequisites

You're going to need:

 - **Linux or OS X** — Windows may work, but is unsupported.
 - **Ruby, version 2.3.1 or newer**
 - **Bundler** — If Ruby is already installed, but the `bundle` command doesn't work, just run `gem install bundler` in a terminal.


To run the server locally:

```shell
bundle install
bundle exec middleman server
```

The doc is then available at http://localhost:4567.
[Editing Slate markdown](https://github.com/lord/slate/wiki/Markdown-Syntax)

### Deploy

Travis will take care about building the static files and deploy them on `surge`.

To generate the static files locally:
```shell
bundle exec middleman build --clean
```
