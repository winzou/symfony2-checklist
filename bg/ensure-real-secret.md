Ensure real secret
security
Ensure that your production server is using a customized secret key. Check it in your `app/config/parameters.yml` file:

    secret:  please_use_a_real_secret_here

The default secret is *not* truly secret, you *must* change it by a random one.
