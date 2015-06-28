# passport-local-fluxible

[Fluxible](http://fluxible.io/) compatible [Passport](http://passportjs.org/)
strategy for authenticating with a username and password.

This is a port of the official [local strategy](https://github.com/jaredhanson/passport-local) to make it work with the Fluxible framework.

## Install

    $ npm install passport-local-fluxible

## Usage

#### Configure Strategy

The local authentication strategy authenticates users using a username and
password.  The strategy requires a `verify` callback, which accepts these
credentials and calls `done` providing a user.

    passport.use(new LocalStrategy(
      function(username, password, done) {
        User.findOne({ username: username }, function (err, user) {
          if (err) { return done(err); }
          if (!user) { return done(null, false); }
          if (!user.verifyPassword(password)) { return done(null, false); }
          return done(null, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'local'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    module.exports = {
      name: 'login',
      create: function(req, resource, params, body, config, done) {
        passport.authenticate('local', function(err, user, info) {
          if(err || !user) {
            debug('Auth failed');
            return done(err);
          }

          req.logIn(user, function(err2) {
            if(err2) {
              debug('Login failed');
              return done(err2);
            }

            return done(err, {
              user: user
            });
          });
        })(req, req.res, done);
      }
    };

## Credits

  - [Jared Hanson](http://github.com/jaredhanson) for the original passport-local
  - [Tommy Leunen](http://github.com/tleunen)

## License

[The MIT License](http://opensource.org/licenses/MIT)