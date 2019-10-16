<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="51764-101">In dieser Übung erweitern Sie die Anwendung aus der vorherigen Übung, um die Authentifizierung mit Azure AD zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="51764-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="51764-102">Dies ist erforderlich, um das erforderliche OAuth-Zugriffstoken zum Aufrufen von Microsoft Graph zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="51764-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="51764-103">Hierzu integrieren Sie die Bibliothek " [Reaktions-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) " in die Anwendung.</span><span class="sxs-lookup"><span data-stu-id="51764-103">To do this, you will integrate the [react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) library into the application.</span></span>

1. <span data-ttu-id="51764-104">Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **auth**.</span><span class="sxs-lookup"><span data-stu-id="51764-104">Create a new directory in the **GraphTutorial** directory named **auth**.</span></span>
1. <span data-ttu-id="51764-105">Erstellen Sie eine neue Datei im **GraphTutorial/auth-** Verzeichnis mit dem Namen **AuthConfig. js**.</span><span class="sxs-lookup"><span data-stu-id="51764-105">Create a new file in the **GraphTutorial/auth** directory named **AuthConfig.js**.</span></span> <span data-ttu-id="51764-106">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="51764-106">Add the following code to the file.</span></span>

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

    <span data-ttu-id="51764-107">Ersetzen `YOUR_APP_ID_HERE` Sie durch die APP-ID aus Ihrer APP-Registrierung.</span><span class="sxs-lookup"><span data-stu-id="51764-107">Replace `YOUR_APP_ID_HERE` with the app ID from your app registration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51764-108">Wenn Sie die Quellcodeverwaltung wie git verwenden, wäre es jetzt ein guter Zeitpunkt, die Datei **AuthConfig. js** aus der Quellcodeverwaltung auszuschließen, um unbeabsichtigtes Auslaufen ihrer APP-ID zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="51764-108">If you're using source control such as git, now would be a good time to exclude the **AuthConfig.js** file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="51764-109">Implementieren der Anmeldung</span><span class="sxs-lookup"><span data-stu-id="51764-109">Implement sign-in</span></span>

<span data-ttu-id="51764-110">In diesem Abschnitt erstellen Sie eine Hilfsklasse für die Authentifizierung und aktualisieren die APP, um sich anzumelden und abzumelden.</span><span class="sxs-lookup"><span data-stu-id="51764-110">In this section you will create an authentication helper class, and update the app to sign in and sign out.</span></span>

1. <span data-ttu-id="51764-111">Erstellen Sie eine neue Datei im **GraphTutorial/auth-** Verzeichnis namens " **AuthManager. js**".</span><span class="sxs-lookup"><span data-stu-id="51764-111">Create a new file in the **GraphTutorial/auth** directory named **AuthManager.js**.</span></span> <span data-ttu-id="51764-112">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="51764-112">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="51764-113">Öffnen Sie die Datei **GraphTutorial/views/SignInScreen. js** , und fügen `import` Sie die folgende Anweisung am Anfang der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="51764-113">Open the **GraphTutorial/views/SignInScreen.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="51764-114">Ersetzen Sie die `_signInAsync` vorhandene Methode durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="51764-114">Replace the existing `_signInAsync` method with the following.</span></span>

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

1. <span data-ttu-id="51764-115">Fügen Sie der Klasse `HomeScreen` die folgende Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="51764-115">Add the following method to the `HomeScreen` class.</span></span>

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

1. <span data-ttu-id="51764-116">Öffnen Sie die Datei **GraphTutorial/Menüs/DrawerMenu. js** , und fügen `import` Sie die folgende Anweisung am Anfang der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="51764-116">Open the **GraphTutorial/menus/DrawerMenu.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="51764-117">Ersetzen `_onItemPressed`Sie in die `// TEMPORARY` folgende Stelle:</span><span class="sxs-lookup"><span data-stu-id="51764-117">In `_onItemPressed`, replace the `// TEMPORARY` line with the following.</span></span>

    ```js
    await AuthManager.signOutAsync();
    ```

1. <span data-ttu-id="51764-118">Speichern Sie Ihre Änderungen, und laden Sie die Anwendung in Ihrem Emulator erneut.</span><span class="sxs-lookup"><span data-stu-id="51764-118">Save your changes and reload the application in your emulator.</span></span>

<span data-ttu-id="51764-119">Wenn Sie sich bei der App anmelden, sollte auf der **Willkommens** Seite ein Zugriffstoken angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="51764-119">If you sign in to the app, you should see an access token displayed on the **Welcome** screen.</span></span>

## <a name="get-user-details"></a><span data-ttu-id="51764-120">Abrufen von Benutzer Details</span><span class="sxs-lookup"><span data-stu-id="51764-120">Get user details</span></span>

<span data-ttu-id="51764-121">In diesem Abschnitt erstellen Sie einen benutzerdefinierten Authentifizierungsanbieter für die Graph-Clientbibliothek, erstellen eine Hilfsklasse zum Aufbewahren aller Aufrufe von Microsoft Graph und aktualisieren `HomeScreen` die `DrawerMenuContent` und-Klassen, um diese neue Klasse zum Abrufen des angemeldeten Benutzers zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="51764-121">In this section you will create a custom authentication provider for the Graph client library, create a helper class to hold all of the calls to Microsoft Graph and update the `HomeScreen` and `DrawerMenuContent` classes to use this new class to get the logged-in user.</span></span>

1. <span data-ttu-id="51764-122">Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Graph**.</span><span class="sxs-lookup"><span data-stu-id="51764-122">Create a new directory in the **GraphTutorial** directory named **graph**.</span></span>
1. <span data-ttu-id="51764-123">Erstellen Sie eine neue Datei im **GraphTutorial/Graph-** Verzeichnis mit dem Namen **GraphAuthProvider. js**.</span><span class="sxs-lookup"><span data-stu-id="51764-123">Create a new file in the **GraphTutorial/graph** directory named **GraphAuthProvider.js**.</span></span> <span data-ttu-id="51764-124">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="51764-124">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="51764-125">Erstellen Sie eine neue Datei im **GraphTutorial/Graph-** Verzeichnis mit dem Namen **graphmanager. js**.</span><span class="sxs-lookup"><span data-stu-id="51764-125">Create a new file in the **GraphTutorial/graph** directory named **GraphManager.js**.</span></span> <span data-ttu-id="51764-126">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="51764-126">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="51764-127">Öffnen Sie die Datei **GraphTutorial/views/homescreen. js** , und fügen `import` Sie die folgende Anweisung am Anfang der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="51764-127">Open the **GraphTutorial/views/HomeScreen.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="51764-128">Ersetzen Sie `componentDidMount` die-Methode durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="51764-128">Replace the `componentDidMount` method with the following.</span></span>

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

1. <span data-ttu-id="51764-129">Öffnen Sie die Datei **GraphTutorial/views/DrawerMenu. js** , und fügen `import` Sie die folgende Anweisung am Anfang der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="51764-129">Open the **GraphTutorial/views/DrawerMenu.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="51764-130">Fügen Sie der `componentDidMount` - `DrawerMenuContent` Klasse die folgende Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="51764-130">Add the following `componentDidMount` method to the `DrawerMenuContent` class.</span></span>

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

<span data-ttu-id="51764-131">Wenn Sie Ihre Änderungen speichern und die APP jetzt erneut laden, wird die Benutzeroberfläche nach der Anmeldung mit dem Anzeigenamen und der e-Mail-Adresse des Benutzers aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="51764-131">If you save your changes and reload the app now, after sign-in the UI is updated with the user's display name and email address.</span></span>
