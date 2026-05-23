#### OAuth Integration

#### How does using the `state` parameter, as recommended, prevent Cross-Site Request Forgery (CSRF) attack on an OAuth flow?

When the user clicks the "Login with Google" and and Google sends the authorization code back to the user, A Cross-Site Request Forgery (CSRF) attack is the one where the browser consuming the authorization code is diffrent from the one that initiated the flow. THe attacker coerces the victim into consuming the attacker's authorization code, causing the victimg to connect with the attacker's suthorizaton context. In makes the user to end up logged into the attacker's account withour reliazing it and anything that is saved such as the card info or upload files etc goes straight intothier account.

The state parameter fixes this by acting ike a secret handshake. Its an  opaque value the client uses to maintain state between the request and the callback. THe authroization server includes this value when reditecting the user-agent back to the client, and it should be used for preventing CSRF. So when your app starts the login flow, it generates a randow token , stores it locally, and sends it to Google. When Google redirects back, your app checks: whether the state value in this response match what the app sent. If it doesnot match like when someone else's code sneaks in - the flow is rejected. The attackers's baton gets dropped

##### Describe a hypothetical scenario where a “leaky” `redirect_uri` validation (e.g., one that allows any path on a valid domain) could be exploited to steal an authorization code.
