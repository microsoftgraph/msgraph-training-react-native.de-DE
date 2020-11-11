<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="1b82d-101">In dieser Übung erweitern Sie die Anwendung aus der vorherigen Übung, um die Authentifizierung mit Azure AD zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="1b82d-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="1b82d-102">Dies ist erforderlich, um das erforderliche OAuth-Zugriffstoken zum Aufrufen von Microsoft Graph zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="1b82d-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="1b82d-103">Hierzu integrieren Sie die Bibliothek " [Reaktions-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) " in die Anwendung.</span><span class="sxs-lookup"><span data-stu-id="1b82d-103">To do this, you will integrate the [react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) library into the application.</span></span>

1. <span data-ttu-id="1b82d-104">Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **auth**.</span><span class="sxs-lookup"><span data-stu-id="1b82d-104">Create a new directory in the **GraphTutorial** directory named **auth**.</span></span>
1. <span data-ttu-id="1b82d-105">Erstellen Sie eine neue Datei im **GraphTutorial/auth-** Verzeichnis mit dem Namen **AuthConfig. TS**.</span><span class="sxs-lookup"><span data-stu-id="1b82d-105">Create a new file in the **GraphTutorial/auth** directory named **AuthConfig.ts**.</span></span> <span data-ttu-id="1b82d-106">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="1b82d-106">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthConfig.example.ts":::

    <span data-ttu-id="1b82d-107">Ersetzen `YOUR_APP_ID_HERE` Sie durch die APP-ID aus Ihrer APP-Registrierung.</span><span class="sxs-lookup"><span data-stu-id="1b82d-107">Replace `YOUR_APP_ID_HERE` with the app ID from your app registration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b82d-108">Wenn Sie die Quellcodeverwaltung wie git verwenden, wäre es jetzt ein guter Zeitpunkt, die Datei **AuthConfig. TS** aus der Quellcodeverwaltung auszuschließen, um unbeabsichtigtes Auslaufen ihrer APP-ID zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="1b82d-108">If you're using source control such as git, now would be a good time to exclude the **AuthConfig.ts** file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="1b82d-109">Implementieren der Anmeldung</span><span class="sxs-lookup"><span data-stu-id="1b82d-109">Implement sign-in</span></span>

<span data-ttu-id="1b82d-110">In diesem Abschnitt erstellen Sie eine Hilfsklasse für die Authentifizierung und aktualisieren die APP, um sich anzumelden und abzumelden.</span><span class="sxs-lookup"><span data-stu-id="1b82d-110">In this section you will create an authentication helper class, and update the app to sign in and sign out.</span></span>

1. <span data-ttu-id="1b82d-111">Erstellen Sie eine neue Datei im **GraphTutorial/auth-** Verzeichnis namens " **AuthManager. TS** ".</span><span class="sxs-lookup"><span data-stu-id="1b82d-111">Create a new file in the **GraphTutorial/auth** directory named **AuthManager.ts**.</span></span> <span data-ttu-id="1b82d-112">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="1b82d-112">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthManager.ts" id="AuthManagerSnippet":::

1. <span data-ttu-id="1b82d-113">Öffnen Sie die Datei **GraphTutorial/app. TSX** , und fügen Sie die folgende `import` Anweisung am Anfang der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="1b82d-113">Open the **GraphTutorial/App.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { AuthManager } from './auth/AuthManager';
    ```

1. <span data-ttu-id="1b82d-114">Ersetzen Sie die vorhandene `authContext` Deklaration durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="1b82d-114">Replace the existing `authContext` declaration with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AuthContextSnippet" highlight="4-6,9":::

1. <span data-ttu-id="1b82d-115">Öffnen Sie die Datei **GraphTutorial/Menus/DrawerMenu. TSX** , und fügen Sie die folgende `import` Anweisung am Anfang der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="1b82d-115">Open the **GraphTutorial/menus/DrawerMenu.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="1b82d-116">Fügen Sie der-Funktion den folgenden Code hinzu `componentDidMount` .</span><span class="sxs-lookup"><span data-stu-id="1b82d-116">Add the following code to the `componentDidMount` function.</span></span>

    ```typescript
    try {
      const accessToken = await AuthManager.getAccessTokenAsync();

      // TEMPORARY
      this.setState({userFirstName: accessToken, userLoading: false});
    } catch (error) {
      Alert.alert(
        'Error getting token',
        JSON.stringify(error),
        [
          {
            text: 'OK'
          }
        ],
        { cancelable: false }
      );
    }
    ```

1. <span data-ttu-id="1b82d-117">Speichern Sie Ihre Änderungen, und laden Sie die Anwendung in Ihrem Emulator erneut.</span><span class="sxs-lookup"><span data-stu-id="1b82d-117">Save your changes and reload the application in your emulator.</span></span>

<span data-ttu-id="1b82d-118">Wenn Sie sich bei der App anmelden, sollte auf der **Willkommens** Seite ein Zugriffstoken angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="1b82d-118">If you sign in to the app, you should see an access token displayed on the **Welcome** screen.</span></span>

## <a name="get-user-details"></a><span data-ttu-id="1b82d-119">Benutzerdetails abrufen</span><span class="sxs-lookup"><span data-stu-id="1b82d-119">Get user details</span></span>

<span data-ttu-id="1b82d-120">In diesem Abschnitt erstellen Sie einen benutzerdefinierten Authentifizierungsanbieter für die Graph-Clientbibliothek, erstellen Sie eine Hilfsklasse, die alle Aufrufe von Microsoft Graph enthält, und aktualisieren Sie die `DrawerMenuContent` Klasse, um die neue Klasse zum Abrufen des angemeldeten Benutzers zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="1b82d-120">In this section you will create a custom authentication provider for the Graph client library, create a helper class to hold all of the calls to Microsoft Graph and update the `DrawerMenuContent` class to use this new class to get the logged-in user.</span></span>

1. <span data-ttu-id="1b82d-121">Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Graph**.</span><span class="sxs-lookup"><span data-stu-id="1b82d-121">Create a new directory in the **GraphTutorial** directory named **graph**.</span></span>
1. <span data-ttu-id="1b82d-122">Erstellen Sie eine neue Datei im **GraphTutorial/Graph-** Verzeichnis mit dem Namen **GraphAuthProvider. TS**.</span><span class="sxs-lookup"><span data-stu-id="1b82d-122">Create a new file in the **GraphTutorial/graph** directory named **GraphAuthProvider.ts**.</span></span> <span data-ttu-id="1b82d-123">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="1b82d-123">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphAuthProvider.ts" id="AuthProviderSnippet":::

1. <span data-ttu-id="1b82d-124">Erstellen Sie eine neue Datei im **GraphTutorial/Graph-** Verzeichnis mit dem Namen **graphmanager. TS**.</span><span class="sxs-lookup"><span data-stu-id="1b82d-124">Create a new file in the **GraphTutorial/graph** directory named **GraphManager.ts**.</span></span> <span data-ttu-id="1b82d-125">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="1b82d-125">Add the following code to the file.</span></span>

    ```typescript
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
        return await graphClient
          .api('/me')
          .select('displayName,givenName,mail,mailboxSettings,userPrincipalName')
          .get();
      }
    }
    ```

1. <span data-ttu-id="1b82d-126">Öffnen Sie die Datei **GraphTutorial/views/DrawerMenu. TSX** , und fügen Sie die folgende `import` Anweisung am Anfang der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="1b82d-126">Open the **GraphTutorial/views/DrawerMenu.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="1b82d-127">Ersetzen Sie die `componentDidMount` -Methode durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="1b82d-127">Replace the `componentDidMount` method with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="ComponentDidMountSnippet":::

<span data-ttu-id="1b82d-128">Wenn Sie Ihre Änderungen speichern und die APP jetzt erneut laden, wird die Benutzeroberfläche nach der Anmeldung mit dem Anzeigenamen und der e-Mail-Adresse des Benutzers aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="1b82d-128">If you save your changes and reload the app now, after sign-in the UI is updated with the user's display name and email address.</span></span>
