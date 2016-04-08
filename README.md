#Authentication

## Getting Application credentials

You will need to reach out to DowJones to get your clientID, clientSecret and establish
your callback URL.  Once you have set these values, you can get to them by going
to your [Dow Jones Client Settings](https://dowjones.com/page-to-be-defined)

## Installation

	npm install passport-dowjones
	npm install express

## Configuration

Take your credentials from the [Dow Jones Client Settings](https://dowjones.com/page-to-be-defined) section described above and initialize the strategy as follows:

~~~js
var DowJonesStrategy = require('passport-dowjones'),
    passport = require('passport');

var strategy = new DowJonesStrategy({
   clientID:     'your-client-id',
   clientSecret: 'your-client-secret',
   callbackURL:  '/callback'
  },
  function(accessToken, refreshToken, extraParams, profile, done) {
    // accessToken is the token to call Auth0 API (not needed in the most cases)
    // extraParams.id_token has the JSON Web Token
    // profile has all the information from the user
    return done(null, profile);
  }
);

passport.use(strategy);
~~~

## Usage

~~~js
app.get('/callback',
  passport.authenticate('dowjones', { failureRedirect: '/login' }),
  function(req, res) {
    if (!req.user) {
      throw new Error('user null');
    }
    res.redirect("/");
  }
);

app.get('/login',
  passport.authenticate('dowjones', {connection: 'PIB-Connection'}), function (req, res) {
  res.redirect("/");
});
~~~

This way when you go to ```/login``` you will get redirected to auth0, to a page where you can select the identity provider.

## Complete example

A complete example of using this library [here](http://github.com/dowjones/passport-dowjones-sample).

## Documentation

For more information about [DowJones](http://dowjones.com) contact our [documentation page](http://dowjones.com/tbd).

## Author

[Dow Jones](dowjones.com)

## License

This project is licensed under the MIT license. See the [LICENSE](LICENSE) file for more info.
