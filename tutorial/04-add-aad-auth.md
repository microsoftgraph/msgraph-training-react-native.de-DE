<!-- markdownlint-disable MD002 MD041 -->

In dieser Übung erweitern Sie die Anwendung aus der vorherigen Übung, um die Authentifizierung mit Azure AD zu unterstützen. Dies ist erforderlich, um das erforderliche OAuth-Zugriffstoken zum Aufrufen von Microsoft Graph zu erhalten. Hierzu integrieren Sie die Bibliothek " [Reaktions-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) " in die Anwendung.

1. Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **auth**.
1. Erstellen Sie eine neue Datei im **GraphTutorial/auth-** Verzeichnis mit dem Namen **AuthConfig. js**. Fügen Sie den folgenden Code in die Datei ein:

    ```js
    export const AuthConfig = {
      appId = 'YOUR_APP_ID_HERE',
      appScopes = [
        'openid',
        'offline_access',
        'profile',
        'User.Read',
        'Calendars.Read'
      ]
    };
    ```

    Ersetzen `YOUR_APP_ID_HERE` Sie durch die APP-ID aus Ihrer APP-Registrierung.

> [!IMPORTANT]
> Wenn Sie die Quellcodeverwaltung wie git verwenden, wäre es jetzt ein guter Zeitpunkt, die Datei **AuthConfig. js** aus der Quellcodeverwaltung auszuschließen, um unbeabsichtigtes Auslaufen ihrer APP-ID zu vermeiden.

## <a name="implement-sign-in"></a>Implementieren der Anmeldung

In diesem Abschnitt erstellen Sie eine Hilfsklasse für die Authentifizierung und aktualisieren die APP, um sich anzumelden und abzumelden.

1. Erstellen Sie eine neue Datei im **GraphTutorial/auth-** Verzeichnis namens " **AuthManager. js**". Fügen Sie den folgenden Code in die Datei ein:

    ```js
    import { AuthConfig } from './AuthConfig';
    import { AsyncStorage } from 'react-native';
    import { authorize, refresh } from 'react-native-app-auth';
    import moment from 'moment';

    const config = {
      clientId: AuthConfig.appId,
      redirectUrl: Platform.OS === 'ios' ? 'urn:ietf:wg:oauth:2.0:oob' : 'graph-tutorial://react-native-auth',
      scopes: AuthConfig.appScopes,
      additionalParameters: { prompt: 'select_account' },
      serviceConfiguration: {
        authorizationEndpoint: 'https://login.microsoftonline.com/common/oauth2/v2.0/authorize',
        tokenEndpoint: 'https://login.microsoftonline.com/common/oauth2/v2.0/token',
      }
    };

    export class AuthManager {

      static signInAsync = async () => {
        const result = await authorize(config);

        // Store the access token, refresh token, and expiration time in storage
        await AsyncStorage.setItem('userToken', result.accessToken);
        await AsyncStorage.setItem('refreshToken', result.refreshToken);
        await AsyncStorage.setItem('expireTime', result.accessTokenExpirationDate);
      }

      static signOutAsync = async () => {
        // Clear storage
        await AsyncStorage.removeItem('userToken');
        await AsyncStorage.removeItem('refreshToken');
        await AsyncStorage.removeItem('expireTime');
      }

      static getAccessTokenAsync = async() => {
        const expireTime = await AsyncStorage.getItem('expireTime');

        if (expireTime !== null) {
          // Get expiration time - 5 minutes
          // If it's <= 5 minutes before expiration, then refresh
          const expire = moment(expireTime).subtract(5, 'minutes');
          const now = moment();

          if (now.isSameOrAfter(expire)) {
            // Expired, refresh
            const refreshToken = await AsyncStorage.getItem('refreshToken');

            const result = await refresh(config, {refreshToken: refreshToken});

            // Store the new access token, refresh token, and expiration time in storage
            await AsyncStorage.setItem('userToken', result.accessToken);
            await AsyncStorage.setItem('refreshToken', result.refreshToken);
            await AsyncStorage.setItem('expireTime', result.accessTokenExpirationDate);

            return result.accessToken;
          }

          // Not expired, just return saved access token
          const accessToken = await AsyncStorage.getItem('userToken');
          return accessToken;
        }

        return null;
      }
    }
    ```

1. Öffnen Sie die Datei **GraphTutorial/views/SignInScreen. js** , und fügen `import` Sie die folgende Anweisung am Anfang der Datei hinzu.

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. Ersetzen Sie die `_signInAsync` vorhandene Methode durch Folgendes.

    ```js
    _signInAsync = async () => {
      try {
        await AuthManager.signInAsync();
        this.props.navigation.navigate('App');
      } catch (error) {
        alert(error);
      }
    };

1. Open the **GraphTutorial/views/HomeScreen.js** file and add the following `import` statement to the top of the file.

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. Fügen Sie der Klasse `HomeScreen` die folgende Methode hinzu.

    ```js
    async componentDidMount() {
      try {
        const accessToken = await AuthManager.getAccessTokenAsync();

        // TEMPORARY
        this.setState({userName: accessToken, userLoading: false});
      } catch (error) {
        alert(error);
      }
    }
    ```

1. Öffnen Sie die Datei **GraphTutorial/Menüs/DrawerMenu. js** , und fügen `import` Sie die folgende Anweisung am Anfang der Datei hinzu.

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. Ersetzen `_onItemPressed`Sie in die `// TEMPORARY` folgende Stelle:

    ```js
    await AuthManager.signOutAsync();
    ```

1. Speichern Sie Ihre Änderungen, und laden Sie die Anwendung in Ihrem Emulator erneut.

Wenn Sie sich bei der App anmelden, sollte auf der **Willkommens** Seite ein Zugriffstoken angezeigt werden.

## <a name="get-user-details"></a>Abrufen von Benutzer Details

In diesem Abschnitt erstellen Sie einen benutzerdefinierten Authentifizierungsanbieter für die Graph-Clientbibliothek, erstellen eine Hilfsklasse zum Aufbewahren aller Aufrufe von Microsoft Graph und aktualisieren `HomeScreen` die `DrawerMenuContent` und-Klassen, um diese neue Klasse zum Abrufen des angemeldeten Benutzers zu verwenden.

1. Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Graph**.
1. Erstellen Sie eine neue Datei im **GraphTutorial/Graph-** Verzeichnis mit dem Namen **GraphAuthProvider. js**. Fügen Sie den folgenden Code in die Datei ein:

    ```js
    import { AuthManager } from '../auth/AuthManager';

    // Used by Graph client to get access tokens
    // See https://github.com/microsoftgraph/msgraph-sdk-javascript/blob/dev/docs/CustomAuthenticationProvider.md
    export class GraphAuthProvider {
      getAccessToken = async() => {
        return await AuthManager.getAccessTokenAsync();
      }
    }
    ```

1. Erstellen Sie eine neue Datei im **GraphTutorial/Graph-** Verzeichnis mit dem Namen **graphmanager. js**. Fügen Sie den folgenden Code in die Datei ein:

    ```js
    import { Client } from '@microsoft/microsoft-graph-client';
    import { GraphAuthProvider } from './GraphAuthProvider';

    // Set the authProvider to an instance
    // of GraphAuthProvider
    const clientOptions = {
      authProvider: new GraphAuthProvider()
    };

    // Initialize the client
    const graphClient = Client.initWithMiddleware(clientOptions);

    export class GraphManager {
      static getUserAsync = async() => {
        // GET /me
        return graphClient.api('/me').get();
      }
    }
    ```

1. Öffnen Sie die Datei **GraphTutorial/views/homescreen. js** , und fügen `import` Sie die folgende Anweisung am Anfang der Datei hinzu.

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. Ersetzen Sie `componentDidMount` die-Methode durch Folgendes.

    ```js
    async componentDidMount() {
      try {
        // Get the signed-in user from Graph
        const user = await GraphManager.getUserAsync();
        // Set the user name to the user's given name
        this.setState({userName: user.givenName, userLoading: false});
      } catch (error) {
        alert(error);
      }
    }
    ```

1. Öffnen Sie die Datei **GraphTutorial/views/DrawerMenu. js** , und fügen `import` Sie die folgende Anweisung am Anfang der Datei hinzu.

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. Fügen Sie der `componentDidMount` - `DrawerMenuContent` Klasse die folgende Methode hinzu.

    ```js
    async componentDidMount() {
      try {
        // Get the signed-in user from Graph
        const user = await GraphManager.getUserAsync();

        // Update UI with display name and email
        this.setState({
          userName: user.displayName,
          // Work/School accounts have email address in mail attribute
          // Personal accounts have it in userPrincipalName
          userEmail: user.mail !== null ? user.mail : user.userPrincipalName,
        });
      } catch(error) {
        alert(error);
      }
    }
    ```

Wenn Sie Ihre Änderungen speichern und die APP jetzt erneut laden, wird die Benutzeroberfläche nach der Anmeldung mit dem Anzeigenamen und der e-Mail-Adresse des Benutzers aktualisiert.
