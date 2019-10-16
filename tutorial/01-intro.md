<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="5de4e-101">In diesem Lernprogramm erfahren Sie, wie Sie eine Reaktionssystem eigene APP erstellen, die die Microsoft Graph-API zum Abrufen von Kalenderinformationen für einen Benutzer verwendet.</span><span class="sxs-lookup"><span data-stu-id="5de4e-101">This tutorial teaches you how to build an React Native app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="5de4e-102">Wenn Sie das fertige Lernprogramm einfach herunterladen möchten, können Sie das GitHub- [Repository](https://github.com/microsoftgraph/msgraph-training-react-native)herunterladen oder Klonen.</span><span class="sxs-lookup"><span data-stu-id="5de4e-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-react-native).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5de4e-103">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="5de4e-103">Prerequisites</span></span>

<span data-ttu-id="5de4e-104">Bevor Sie mit diesem Lernprogramm beginnen, sollten Sie Folgendes auf Ihrem Entwicklungscomputer installiert haben.</span><span class="sxs-lookup"><span data-stu-id="5de4e-104">Before you start this tutorial, you should have the following installed on your development machine.</span></span>

- <span data-ttu-id="5de4e-105">Mindestens eine der folgenden:</span><span class="sxs-lookup"><span data-stu-id="5de4e-105">At least one of the following:</span></span>
  - <span data-ttu-id="5de4e-106">[Android Studio](https://developer.android.com/studio/) **und** [Java Development Kit](https://jdk.java.net) (erforderlich zum Ausführen des Beispiels unter Android)</span><span class="sxs-lookup"><span data-stu-id="5de4e-106">[Android Studio](https://developer.android.com/studio/) **and** [Java Development Kit](https://jdk.java.net) (required to run the sample on Android)</span></span>
  - <span data-ttu-id="5de4e-107">[Xcode](https://developer.apple.com/xcode/) (erforderlich zum Ausführen des Beispiels unter IOS)</span><span class="sxs-lookup"><span data-stu-id="5de4e-107">[Xcode](https://developer.apple.com/xcode/) (required to run the sample on iOS)</span></span>
- [<span data-ttu-id="5de4e-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="5de4e-108">Node.js</span></span>](https://nodejs.org)

> [!NOTE]
> <span data-ttu-id="5de4e-109">Dieses Lernprogramm wurde mithilfe der nativen CLI-Reaktions Software geschrieben, die je nach Betriebssystem und Zielplattform spezifische Voraussetzungen hat.</span><span class="sxs-lookup"><span data-stu-id="5de4e-109">This tutorial was written using the React Native CLI, which has specific prerequisites depending on your operating system and target platforms.</span></span> <span data-ttu-id="5de4e-110">Anweisungen zum Konfigurieren des Entwicklungscomputers finden Sie unter [reagieren systemeigene erste Schritte](https://facebook.github.io/react-native/docs/getting-started) .</span><span class="sxs-lookup"><span data-stu-id="5de4e-110">See [React Native Getting Started](https://facebook.github.io/react-native/docs/getting-started) for instructions on configuring your development machine.</span></span> <span data-ttu-id="5de4e-111">Die für dieses Lernprogramm verwendeten Versionen sind unten aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="5de4e-111">The versions used for this tutorial are listed below.</span></span> <span data-ttu-id="5de4e-112">Die Schritte in diesem Leitfaden funktionieren möglicherweise mit anderen Versionen, jedoch nicht getestet.</span><span class="sxs-lookup"><span data-stu-id="5de4e-112">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="5de4e-113">Android Studio Version 3.4.2 mit dem 1.8.0 JRE und dem Android 9,0 SDK</span><span class="sxs-lookup"><span data-stu-id="5de4e-113">Android Studio version 3.4.2 with the 1.8.0 JRE and the Android 9.0 SDK</span></span>
> - <span data-ttu-id="5de4e-114">Java Development Kit-Version 12.0.2</span><span class="sxs-lookup"><span data-stu-id="5de4e-114">Java Development Kit version 12.0.2</span></span>
> - <span data-ttu-id="5de4e-115">Xcode Version 10,3</span><span class="sxs-lookup"><span data-stu-id="5de4e-115">Xcode version 10.3</span></span>
> - <span data-ttu-id="5de4e-116">Node. js-Version 10.16.0</span><span class="sxs-lookup"><span data-stu-id="5de4e-116">Node.js version 10.16.0</span></span>

## <a name="feedback"></a><span data-ttu-id="5de4e-117">Feedback</span><span class="sxs-lookup"><span data-stu-id="5de4e-117">Feedback</span></span>

<span data-ttu-id="5de4e-118">Geben Sie Feedback zu diesem Lernprogramm im [GitHub-Repository](https://github.com/microsoftgraph/msgraph-training-react-native)an.</span><span class="sxs-lookup"><span data-stu-id="5de4e-118">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-react-native).</span></span>
