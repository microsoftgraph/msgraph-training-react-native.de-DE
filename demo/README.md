# <a name="how-to-run-the-completed-project"></a>Vorgehensweise Ausführen des abgeschlossenen Projekts

## <a name="prerequisites"></a>Voraussetzungen

Um das abgeschlossene Projekt in diesem Ordner auszuführen, benötigen Sie Folgendes:

- Mindestens eine der folgenden:
  - [Android Studio](https://developer.android.com/studio/) **und** [Java Development Kit](https://jdk.java.net) (erforderlich zum Ausführen des Beispiels unter Android)
  - [Xcode](https://developer.apple.com/xcode/) (erforderlich zum Ausführen des Beispiels unter IOS)
- [Node.js](https://nodejs.org)
- Entweder ein persönliches Microsoft-Konto mit einem Postfach auf Outlook.com oder ein Microsoft-Arbeits-oder Schulkonto.

> **Hinweis:** Dieses Lernprogramm wurde mithilfe der nativen CLI-Reaktions Software geschrieben, die je nach Betriebssystem und Zielplattform spezifische Voraussetzungen hat. Anweisungen zum Konfigurieren des Entwicklungscomputers finden Sie unter [reagieren systemeigene erste Schritte](https://facebook.github.io/react-native/docs/getting-started) . Die für dieses Lernprogramm verwendeten Versionen sind unten aufgeführt. Die Schritte in diesem Leitfaden funktionieren möglicherweise mit anderen Versionen, jedoch nicht getestet.
>
> - Android Studio Version 4,1 mit dem Android 9,0 SDK
> - Java Development Kit-Version 12.0.2
> - Xcode Version 12,1
> - Node.js Version 14.15.0

Wenn Sie kein Microsoft-Konto haben, gibt es mehrere Optionen, um ein kostenloses Konto zu erhalten:

- Sie können [sich für ein neues persönliches Microsoft-Konto registrieren](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).
- Sie können sich [für das Office 365 Entwicklerprogramm registrieren](https://developer.microsoft.com/office/dev-program) , um ein kostenloses Office 365-Abonnement zu erhalten.

## <a name="register-an-application-with-the-azure-active-directory-admin-center"></a>Registrieren einer Anwendung im Azure Active Directory Admin Center

1. Öffnen Sie einen Browser, und navigieren Sie zum [Azure Active Directory Admin Center](https://aad.portal.azure.com). Melden Sie sich mit einem **persönlichen Konto** (auch: Microsoft-Konto) oder einem **Geschäfts- oder Schulkonto** an.

1. Wählen Sie in der linken Navigationsleiste **Azure Active Directory** aus, und wählen Sie dann **App-Registrierungen** unter **Verwalten** aus.

    ![Screenshot der APP-Registrierungen ](/tutorial/images/aad-portal-app-registrations.png)

1. Wählen Sie **Neue Registrierung** aus. Legen Sie auf der Seite **Anwendung registrieren** die Werte wie folgt fest.

    - Legen Sie **Name** auf `React Native Graph Tutorial` fest.
    - Legen Sie **Unterstützte Kontotypen** auf **Konten in allen Organisationsverzeichnissen und persönliche Microsoft-Konten** fest.
    - Ändern Sie unter **Umleitungs-URI** das Dropdown-Menü auf **Public Client (Mobile & Desktop)** , und legen Sie den Wert auf fest `graph-tutorial://react-native-auth` .

    ![Screenshot der Seite "Anwendung registrieren"](/tutorial/images/aad-register-an-app.png)

1. Wählen Sie **Registrieren** aus. Kopieren Sie auf der Seite **systemeigene Graph-Lernprogramm reagieren** den Wert der **Anwendungs-ID (Client)** , und speichern Sie Sie, um Sie im nächsten Schritt zu benötigen.

    ![Screenshot der Anwendungs-ID der neuen App-Registrierung](/tutorial/images/aad-application-id.png)

1. Wählen Sie unter **Verwalten** die Option **Authentifizierung** aus. Fügen Sie auf der Seite " **Umleitungs-URIs** " einen weiteren Umleitungs-URI vom Typ " **Public Client" (Mobile & Desktop)** mit dem URI hinzu `urn:ietf:wg:oauth:2.0:oob` . Klicken Sie auf **Speichern**.

    ![Screenshot der Seite "Umleitungs-URIs"](/tutorial/images/aad-redirect-uris.png)

## <a name="configure-the-sample"></a>Konfigurieren des Beispiels

1. Benennen Sie die Datei **GraphTutorial/auth/AuthConfig. example. TS** in **AuthConfig. TS** um.
1. Bearbeiten Sie die Datei **AuthConfig. TS** , und nehmen Sie die folgenden Änderungen vor.
    1. Ersetzen `YOUR_APP_ID_HERE` Sie durch die **Anwendungs-ID** , die Sie im App-Registrierungs Portal erhalten haben.

1. Navigieren Sie in der Befehlszeilenschnittstelle (CLI) zum Verzeichnis **GraphTutorial** , und führen Sie den folgenden Befehl aus, um Anforderungen zu installieren.

    ```Shell
    npm install
    ```

1. Navigieren Sie in der Befehlszeilenschnittstelle (CLI) zum **GraphTutorial/IOS** -Verzeichnis, und führen Sie den folgenden Befehl aus, um Anforderungen zu installieren.

    ```Shell
    pod install
    ```

## <a name="run-the-sample"></a>Ausführen des Beispiels

### <a name="run-on-ios-simulator"></a>Auf IOS-Simulator ausführen

Führen Sie den folgenden Befehl in der CLI aus, um die Anwendung in einem IOS-Simulator zu starten.

```Shell
react-native run-ios
```

### <a name="run-on-android-emulator"></a>Ausführen auf Android-Emulator

Starten Sie und Android-Emulator-Instanz, und führen Sie den folgenden Befehl in ihrer CLI aus, um die Anwendung in einem Android-Emulator zu starten.

```Shell
react-native run-android
```
