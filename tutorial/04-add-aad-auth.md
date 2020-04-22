<!-- markdownlint-disable MD002 MD041 -->

In dieser Übung erweitern Sie die Anwendung aus der vorherigen Übung, um die Authentifizierung mit Azure AD zu unterstützen. Dies ist erforderlich, um das erforderliche OAuth-Zugriffstoken zum Aufrufen von Microsoft Graph zu erhalten. Hierzu integrieren Sie die Bibliothek " [Reaktions-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) " in die Anwendung.

1. Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **auth**.
1. Erstellen Sie eine neue Datei im **GraphTutorial/auth-** Verzeichnis mit dem Namen **AuthConfig. TS**. Fügen Sie den folgenden Code in die Datei ein:

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthConfig.ts.example":::

    Ersetzen `YOUR_APP_ID_HERE` Sie durch die APP-ID aus Ihrer APP-Registrierung.

> [!IMPORTANT]
> Wenn Sie die Quellcodeverwaltung wie git verwenden, wäre es jetzt ein guter Zeitpunkt, die Datei **AuthConfig. TS** aus der Quellcodeverwaltung auszuschließen, um unbeabsichtigtes Auslaufen ihrer APP-ID zu vermeiden.

## <a name="implement-sign-in"></a>Implementieren der Anmeldung

In diesem Abschnitt erstellen Sie eine Hilfsklasse für die Authentifizierung und aktualisieren die APP, um sich anzumelden und abzumelden.

1. Erstellen Sie eine neue Datei im **GraphTutorial/auth-** Verzeichnis namens " **AuthManager. TS**". Fügen Sie den folgenden Code in die Datei ein:

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthManager.ts" id="AuthManagerSnippet":::

1. Öffnen Sie die Datei **GraphTutorial/views/SignInScreen. TSX** , und fügen `import` Sie die folgende Anweisung am Anfang der Datei hinzu.

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. Ersetzen Sie die `_signInAsync` vorhandene Methode durch Folgendes.

    :::code language="typescript" source="../demo/GraphTutorial/screens/SignInScreen.tsx" id="SignInAsyncSnippet":::

1. Öffnen Sie die Datei **GraphTutorial/views/homescreen. TSX** , und fügen `import` Sie die folgende Anweisung am Anfang der Datei hinzu.

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. Fügen Sie der Klasse `HomeScreen` die folgende Methode hinzu.

    ```typescript
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

1. Öffnen Sie die Datei **GraphTutorial/Menus/DrawerMenu. TSX** , und `import` fügen Sie die folgende Anweisung am Anfang der Datei hinzu.

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. Ersetzen Sie die `_signOut` vorhandene Methode durch Folgendes.

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="SignOutSnippet" highlight="5":::

1. Speichern Sie Ihre Änderungen, und laden Sie die Anwendung in Ihrem Emulator erneut.

Wenn Sie sich bei der App anmelden, sollte auf der **Willkommens** Seite ein Zugriffstoken angezeigt werden.

## <a name="get-user-details"></a>Benutzerdetails abrufen

In diesem Abschnitt erstellen Sie einen benutzerdefinierten Authentifizierungsanbieter für die Graph-Clientbibliothek, erstellen eine Hilfsklasse zum Aufbewahren aller Aufrufe von Microsoft Graph und aktualisieren `HomeScreen` die `DrawerMenuContent` und-Klassen, um diese neue Klasse zum Abrufen des angemeldeten Benutzers zu verwenden.

1. Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Graph**.
1. Erstellen Sie eine neue Datei im **GraphTutorial/Graph-** Verzeichnis mit dem Namen **GraphAuthProvider. TS**. Fügen Sie den folgenden Code in die Datei ein:

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphAuthProvider.ts" id="AuthProviderSnippet":::

1. Erstellen Sie eine neue Datei im **GraphTutorial/Graph-** Verzeichnis mit dem Namen **graphmanager. TS**. Fügen Sie den folgenden Code in die Datei ein:

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
        return graphClient.api('/me').get();
      }
    }
    ```

1. Öffnen Sie die Datei **GraphTutorial/views/homescreen. TSX** , und fügen `import` Sie die folgende Anweisung am Anfang der Datei hinzu.

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. Ersetzen Sie `componentDidMount` die-Methode durch Folgendes.

    :::code language="typescript" source="../demo/GraphTutorial/screens/HomeScreen.tsx" id="ComponentDidMountSnippet" highlight="3-6,9":::

1. Öffnen Sie die Datei **GraphTutorial/views/DrawerMenu. TSX** , und fügen `import` Sie die folgende Anweisung am Anfang der Datei hinzu.

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. Fügen Sie der Klasse die folgende`componentDidMount` Methode hinzu`DrawerMenuContent`.

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="ComponentDidMountSnippet":::

Wenn Sie Ihre Änderungen speichern und die APP jetzt erneut laden, wird die Benutzeroberfläche nach der Anmeldung mit dem Anzeigenamen und der e-Mail-Adresse des Benutzers aktualisiert.
