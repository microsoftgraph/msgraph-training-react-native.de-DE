# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="c7164-101">Vorgehensweise Ausführen des abgeschlossenen Projekts</span><span class="sxs-lookup"><span data-stu-id="c7164-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7164-102">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="c7164-102">Prerequisites</span></span>

<span data-ttu-id="c7164-103">Um das abgeschlossene Projekt in diesem Ordner auszuführen, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="c7164-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="c7164-104">Mindestens eine der folgenden:</span><span class="sxs-lookup"><span data-stu-id="c7164-104">At least one of the following:</span></span>
  - <span data-ttu-id="c7164-105">[Android Studio](https://developer.android.com/studio/) **und** [Java Development Kit](https://jdk.java.net) (erforderlich zum Ausführen des Beispiels unter Android)</span><span class="sxs-lookup"><span data-stu-id="c7164-105">[Android Studio](https://developer.android.com/studio/) **and** [Java Development Kit](https://jdk.java.net) (required to run the sample on Android)</span></span>
  - <span data-ttu-id="c7164-106">[Xcode](https://developer.apple.com/xcode/) (erforderlich zum Ausführen des Beispiels unter IOS)</span><span class="sxs-lookup"><span data-stu-id="c7164-106">[Xcode](https://developer.apple.com/xcode/) (required to run the sample on iOS)</span></span>
- [<span data-ttu-id="c7164-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="c7164-107">Node.js</span></span>](https://nodejs.org)
- <span data-ttu-id="c7164-108">Entweder ein persönliches Microsoft-Konto mit einem Postfach auf Outlook.com oder ein Microsoft-Arbeits-oder Schulkonto.</span><span class="sxs-lookup"><span data-stu-id="c7164-108">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

> <span data-ttu-id="c7164-109">**Hinweis:** Dieses Lernprogramm wurde mithilfe der nativen CLI-Reaktions Software geschrieben, die je nach Betriebssystem und Zielplattform spezifische Voraussetzungen hat.</span><span class="sxs-lookup"><span data-stu-id="c7164-109">**Note:** This tutorial was written using the React Native CLI, which has specific prerequisites depending on your operating system and target platforms.</span></span> <span data-ttu-id="c7164-110">Anweisungen zum Konfigurieren des Entwicklungscomputers finden Sie unter [reagieren systemeigene erste Schritte](https://facebook.github.io/react-native/docs/getting-started) .</span><span class="sxs-lookup"><span data-stu-id="c7164-110">See [React Native Getting Started](https://facebook.github.io/react-native/docs/getting-started) for instructions on configuring your development machine.</span></span> <span data-ttu-id="c7164-111">Die für dieses Lernprogramm verwendeten Versionen sind unten aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="c7164-111">The versions used for this tutorial are listed below.</span></span> <span data-ttu-id="c7164-112">Die Schritte in diesem Leitfaden funktionieren möglicherweise mit anderen Versionen, jedoch nicht getestet.</span><span class="sxs-lookup"><span data-stu-id="c7164-112">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="c7164-113">Android Studio Version 3.6.2 mit dem Android 9,0 SDK</span><span class="sxs-lookup"><span data-stu-id="c7164-113">Android Studio version 3.6.2 with the Android 9.0 SDK</span></span>
> - <span data-ttu-id="c7164-114">Java Development Kit-Version 12.0.2</span><span class="sxs-lookup"><span data-stu-id="c7164-114">Java Development Kit version 12.0.2</span></span>
> - <span data-ttu-id="c7164-115">Xcode Version 11,4</span><span class="sxs-lookup"><span data-stu-id="c7164-115">Xcode version 11.4</span></span>
> - <span data-ttu-id="c7164-116">Node. js-Version 12.16.2</span><span class="sxs-lookup"><span data-stu-id="c7164-116">Node.js version 12.16.2</span></span>

<span data-ttu-id="c7164-117">Wenn Sie kein Microsoft-Konto haben, gibt es mehrere Optionen, um ein kostenloses Konto zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="c7164-117">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="c7164-118">Sie können [sich für ein neues persönliches Microsoft-Konto registrieren](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span><span class="sxs-lookup"><span data-stu-id="c7164-118">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="c7164-119">Sie können sich [für das Office 365 Entwicklerprogramm registrieren](https://developer.microsoft.com/office/dev-program) , um ein kostenloses Office 365-Abonnement zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="c7164-119">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-an-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="c7164-120">Registrieren einer Anwendung im Azure Active Directory Admin Center</span><span class="sxs-lookup"><span data-stu-id="c7164-120">Register an application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="c7164-121">Öffnen Sie einen Browser, und navigieren Sie zum [Azure Active Directory Admin Center](https://aad.portal.azure.com). Melden Sie sich mit einem **persönlichen Konto** (auch: Microsoft-Konto) oder einem **Geschäfts- oder Schulkonto** an.</span><span class="sxs-lookup"><span data-stu-id="c7164-121">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="c7164-122">Wählen Sie in der linken Navigationsleiste **Azure Active Directory** aus, und wählen Sie dann **App-Registrierungen** unter **Verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="c7164-122">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="c7164-123">Screenshot der APP-Registrierungen</span><span class="sxs-lookup"><span data-stu-id="c7164-123">A screenshot of the App registrations</span></span> ](/tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="c7164-124">Wählen Sie **Neue Registrierung** aus.</span><span class="sxs-lookup"><span data-stu-id="c7164-124">Select **New registration**.</span></span> <span data-ttu-id="c7164-125">Legen Sie auf der Seite **Anwendung registrieren** die Werte wie folgt fest.</span><span class="sxs-lookup"><span data-stu-id="c7164-125">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="c7164-126">Legen Sie **Name** auf `React Native Graph Tutorial` fest.</span><span class="sxs-lookup"><span data-stu-id="c7164-126">Set **Name** to `React Native Graph Tutorial`.</span></span>
    - <span data-ttu-id="c7164-127">Legen Sie **Unterstützte Kontotypen** auf **Konten in allen Organisationsverzeichnissen und persönliche Microsoft-Konten** fest.</span><span class="sxs-lookup"><span data-stu-id="c7164-127">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="c7164-128">Ändern Sie unter **Umleitungs-URI**das Dropdown-Menü auf **Public Client (Mobile & Desktop)**, `graph-tutorial://react-native-auth`und legen Sie den Wert auf fest.</span><span class="sxs-lookup"><span data-stu-id="c7164-128">Under **Redirect URI**, change the dropdown to **Public client (mobile & desktop)**, and set the value to `graph-tutorial://react-native-auth`.</span></span>

    ![Screenshot der Seite "Anwendung registrieren"](/tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="c7164-130">Wählen Sie **Registrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="c7164-130">Select **Register**.</span></span> <span data-ttu-id="c7164-131">Kopieren Sie auf der Seite **systemeigene Graph-Lernprogramm reagieren** den Wert der **Anwendungs-ID (Client)** , und speichern Sie Sie, um Sie im nächsten Schritt zu benötigen.</span><span class="sxs-lookup"><span data-stu-id="c7164-131">On the **React Native Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Screenshot der Anwendungs-ID der neuen App-Registrierung](/tutorial/images/aad-application-id.png)

1. <span data-ttu-id="c7164-133">Wählen Sie unter **Verwalten**die Option **Authentifizierung**aus.</span><span class="sxs-lookup"><span data-stu-id="c7164-133">Under **Manage**, select **Authentication**.</span></span> <span data-ttu-id="c7164-134">Fügen Sie auf der Seite " **Umleitungs-URIs** " einen weiteren Umleitungs-URI vom Typ " **Public Client" (Mobile & Desktop)** mit dem URI `urn:ietf:wg:oauth:2.0:oob`hinzu.</span><span class="sxs-lookup"><span data-stu-id="c7164-134">On the **Redirect URIs** page, add another redirect URI of type **Public client (mobile & desktop)**, with the URI `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="c7164-135">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="c7164-135">Select **Save**.</span></span>

    ![Screenshot der Seite "Umleitungs-URIs"](/tutorial/images/aad-redirect-uris.png)

## <a name="configure-the-sample"></a><span data-ttu-id="c7164-137">Konfigurieren des Beispiels</span><span class="sxs-lookup"><span data-stu-id="c7164-137">Configure the sample</span></span>

1. <span data-ttu-id="c7164-138">Benennen Sie die Datei **GraphTutorial/auth/AuthConfig. TS. example** in **AuthConfig. TS**um.</span><span class="sxs-lookup"><span data-stu-id="c7164-138">Rename the **GraphTutorial/auth/AuthConfig.ts.example** file to **AuthConfig.ts**.</span></span>
1. <span data-ttu-id="c7164-139">Bearbeiten Sie die Datei **AuthConfig. TS** , und nehmen Sie die folgenden Änderungen vor.</span><span class="sxs-lookup"><span data-stu-id="c7164-139">Edit the **AuthConfig.ts** file and make the following changes.</span></span>
    1. <span data-ttu-id="c7164-140">Ersetzen `YOUR_APP_ID_HERE` Sie durch die **Anwendungs-ID** , die Sie im App-Registrierungs Portal erhalten haben.</span><span class="sxs-lookup"><span data-stu-id="c7164-140">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>

1. <span data-ttu-id="c7164-141">Navigieren Sie in der Befehlszeilenschnittstelle (CLI) zum Verzeichnis **GraphTutorial** , und führen Sie den folgenden Befehl aus, um Anforderungen zu installieren.</span><span class="sxs-lookup"><span data-stu-id="c7164-141">In your command-line interface (CLI), navigate to the **GraphTutorial** directory and run the following command to install requirements.</span></span>

    ```Shell
    npm install
    ```

1. <span data-ttu-id="c7164-142">Navigieren Sie in der Befehlszeilenschnittstelle (CLI) zum **GraphTutorial/IOS** -Verzeichnis, und führen Sie den folgenden Befehl aus, um Anforderungen zu installieren.</span><span class="sxs-lookup"><span data-stu-id="c7164-142">In your command-line interface (CLI), navigate to the **GraphTutorial/ios** directory and run the following command to install requirements.</span></span>

    ```Shell
    pod install
    ```

## <a name="run-the-sample"></a><span data-ttu-id="c7164-143">Ausführen des Beispiels</span><span class="sxs-lookup"><span data-stu-id="c7164-143">Run the sample</span></span>

### <a name="run-on-ios-simulator"></a><span data-ttu-id="c7164-144">Auf IOS-Simulator ausführen</span><span class="sxs-lookup"><span data-stu-id="c7164-144">Run on iOS Simulator</span></span>

<span data-ttu-id="c7164-145">Führen Sie den folgenden Befehl in der CLI aus, um die Anwendung in einem IOS-Simulator zu starten.</span><span class="sxs-lookup"><span data-stu-id="c7164-145">Run the following command in your CLI to start the application in an iOS Simulator.</span></span>

```Shell
react-native run-ios
```

### <a name="run-on-android-emulator"></a><span data-ttu-id="c7164-146">Ausführen auf Android-Emulator</span><span class="sxs-lookup"><span data-stu-id="c7164-146">Run on Android emulator</span></span>

<span data-ttu-id="c7164-147">Starten Sie und Android-Emulator-Instanz, und führen Sie den folgenden Befehl in ihrer CLI aus, um die Anwendung in einem Android-Emulator zu starten.</span><span class="sxs-lookup"><span data-stu-id="c7164-147">Launch and Android emulator instance and run the following command in your CLI to start the application in an Android emulator.</span></span>

```Shell
react-native run-android
```
