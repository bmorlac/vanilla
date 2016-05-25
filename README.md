# vanilla

This project is generated with [yo angular generator](https://github.com/yeoman/generator-angular)
version 0.15.1 with just a few Angular libraries included. The main focus was to have a runnable
scaffolded base project out of the box. In the past, running a command like `yo angular vanilla`
did the job. Unfortunately, nowadays the generated Gruntfile leverages Compass, which in turn
requires you to install Ruby. Something what I personally didn't want, precisely because with
[grunt-sass](https://www.npmjs.com/package/grunt-sass) there is already a well-suited library in the
Node.js ecosystem.

Another thing that bothered me was, that the dependencies generated with the current version 0.15.1
of the generator are hopelessly outdated if you consider to use npm@3. Npm will tell you that in an
unmistakeable fashion if you try to run the `npm install` command.

So here's what I did to turn the initially generated project into a runnable app:

1. Bumped the versions of
 - grunt,
 - grunt-contrib-connect,
 - grunt-contrib-copy,
 - grunt-contrib-uglify,
 - grunt-contrib-watch,
 - grunt-jscs,
 - grunt-ng-annotate,
 - grunt-postcss,
 - grunt-wiredep,
 - jit-grunt
  
 to participate from the updated `peerDependencies` sections in the current versions of the plugins.
2. After the upgrade of `grunt-contrib-connect`, the connect tasks in the Gruntfile needed to be
 adjusted, since the API changed. As a consequence I had to `npm install serve-static --save-dev`,
 so I could leverage from it in the `middleware` config blocks.
3. Get rid of the unwanted Grunt Compass plugin and installed `grunt-sass` instead: `npm uninstall
 grunt-contrib-compass --save-dev && npm install grunt-sass --save-dev`.
4. Accordingly, I replaced the remaining config blocks of `grunt-contrib-compass` with those of
 `grunt-sass` in the Gruntfile.
5. Last but not least, I installed Karma and PhantomJS, so that I can run tests:
 `npm install karma grunt-karma karma-phantomjs-launcher karma-jasmine jasmine-core
 phantomjs-prebuilt --save-dev`.

That's it. Hope that saved you some time.

## Build & development

Run `grunt` for building and `grunt serve` for preview.

## Testing

Running `grunt test` will run the unit tests with karma.
