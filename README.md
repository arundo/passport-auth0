This is the auth0 authentication strategy for Passport.js.

## Instalation

	npm install http://bit.ly/passportauth0

## Configuration

~~~js
passport.use(new Auth10Strategy({
   namespace:    'your-namespace.auth0.com',
   clientID: 	 'your-client-id',
   clientSecret: 'your-client-secret',
   callbackURL:  '/callback'
  },
  function(accessToken, refreshToken, profile, done) {
    //do something here with the profile
    return done(null, profile);
  }
));
~~~

## Usage

~~~js
app.get('/callback', 
  passport.authenticate('auth10', { failureRedirect: '/login' }), 
  function(req, res) {
    if (!req.user) {
      throw new Error('user null');
    }
    res.redirect("/");
  }
);

app.get('/login', 
  passport.authenticate('auth10', {connection: 'connection1'}), function (req, res) {
  res.redirect("/");
});
~~~

## Logout

In order to logout we need to do some extra redirection, so it is a little bit different than with vanilla passport.js

~~~js
app.get('/logout', function(req, res){
  req.logout(res, 'http://myapplication.com');
});
~~~

The first parameter is the response and the second parameter is the destination url.