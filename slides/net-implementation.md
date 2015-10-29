## .net Implementation

Inside the Startup class

    public void Configuration(IAppBuilder app)
    {
        var config = new HttpConfiguration();

        var OAuthServerOptions = new OAuthAuthorizationServerOptions
        {
            TokenEndpointPath = new PathString("/token"),
            AccessTokenExpireTimeSpan = TimeSpan.FromHours(1),
            Provider = new CustomAuthorizationServerProvider(),
            RefreshTokenProvider = new CustomRefreshTokenProvider(),
        };

        app.UseOAuthAuthorizationServer(OAuthServerOptions);
        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions());

        // The rest of the configuration
    }

---

CustomAuthorizationServerProvider

    public class CustomAuthorizationServerProvider
        : OAuthAuthorizationServerProvider
    {
        // Called to validate that the origin of the request
        // is a registered "client_id", and that the correct credentials
        // for that client are present on the request
        public override async Task ValidateClientAuthentication(
            OAuthValidateClientAuthenticationContext context)
        {
            string clientId, clientSecret;
            if (!context.TryGetFormCredentials(out clientId, out clientSecret))
            {
                context.TryGetBasicCredentials(out clientId, out clientSecret);
            }
            
            // Get client by clientId
            
            // Validate client
            
            context.Validated(clientId);
        }

        // Called when a request to the Token endpoint arrives with a
        // "grant_type" of "authorization_code"
        public override async Task GrantAuthorizationCode(
            OAuthGrantAuthorizationCodeContext context)
        {
        }

        // Called when a request to the Token endpoint arrives with a
        // "grant_type" of "password"
        public override async Task GrantResourceOwnerCredentials(
            OAuthGrantResourceOwnerCredentialsContext context)
        {
        }

        // Called when a request to the Token endpoint arrives with a
        // "grant_type" of "client_credentials"
        public override async Task GrantClientCredentials(
            OAuthGrantClientCredentialsContext context)
        {
        }

        // Called when a request to the Token endpoint arrives with a
        // "grant_type" of "refresh_token"
        public override async Task GrantRefreshToken(
            OAuthGrantRefreshTokenContext context)
        {
        }
        
        // Called when a request to the Token endpoint arrives with a
        // "grant_type" of any other value
        public override async Task GrantCustomExtension(
            OAuthGrantCustomExtensionContext context)
        {
        }
    }

---

CustomRefreshTokenProvider

    public class CustomRefreshTokenProvider : AuthenticationTokenProvider
    {
        public override async Task CreateAsync(
            AuthenticationTokenCreateContext context)
        {
            // Create a new Refresh Token and persist it the database
        }

        public override async Task ReceiveAsync(
            AuthenticationTokenReceiveContext context)
        {
            // Get the Refresh Token from the database
        }
    }
