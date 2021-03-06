Here you will find status messages, alerts, and errors that should be handled by a partner app.

## Development/Implementation Errors

Errors are implemented as a number of exception classes that will be delivered through callbacks
when they occur. By investigating the type of the error, implementations can choose the right course
of action.

### Connection errors

Connection errors are delivered through the on `onFailure` method of `ConnectionListener`.
Connection errors can occur at any time from that a clients calls `connect` up until the time the
client has disconnected. The following comprises a list of errors that can be delivered through the
`ConnectionListener.onFailure()` callback:

```
   CouldNotFindSpotifyApp
```

The Spotify app is not installed on the device. Guide the user to install [Spotify from Google Play](https://play.google.com/store/apps/details?id=com.spotify.music) and try to
connect again.

```
   NotLoggedInException
```

No one is logged in to the Spotify app on this device. Guide the user to log in to Spotify and try
again.

```
   AuthenticationFailedException
```

Partner app failed to authenticate with Spotify. Check client credentials and make sure your app is
registered correctly at developer.spotify.com

```
   UserNotAuthorizedException
```

Indicates the user did not authorize this client of App Remote to use Spotify on the user[“Authentication
And Authorization”](https://developer.spotifyinternal.com/documentation/android-app-remote/#authentication-and-authorization) section on the Developer Site.

```
   UnsupportedFeatureVersionException
```

Spotify app can't support requested features. User should update Spotify app.

```
   OfflineModeException
```

Spotify user has set their Spotify app to be in offline mode, but app remote requires a call to be
made to the backend. The user needs to disable offline mode in the Spotify app.

```
   LoggedOutException
```

User has logged out from Spotify. The difference between this one and `NotLoggedInException` is that
 in case of the latter the connection could not have been established. `LoggedOutException` means
 that user logged out after Remote SDK connected to Spotify app.

```
   SpotifyDisconnectedException
```

The Spotify app was/is disconnected by the Spotify app. This indicates typically that the Spotify
app was closed by the user or for other reasons. You need to reconnect to continue using Spotify App
 Remote.

```
   SpotifyConnectionTerminatedException
```

The connection to the Spotify app was unexpectedly terminated. Spotify might have crashed or was
killed by the system. You need to reconnect to continue using Spotify App Remote.

```
   RemoteClientException
```

Your requested call was not successful. The message will explain what type of action was unsuccessful and the reason why.
For example, trying to initiate playback with a bad URI would return 
`com.spotify.protocol.client.error.RemoteClientException: {"message":"Cannot play specified uri": [NOT_A_VALID_URI]"}`