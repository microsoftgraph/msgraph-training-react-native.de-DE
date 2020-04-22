<!-- markdownlint-disable MD002 MD041 -->

In diesem Lernprogramm erfahren Sie, wie Sie eine Reaktionssystem eigene APP erstellen, die die Microsoft Graph-API zum Abrufen von Kalenderinformationen für einen Benutzer verwendet.

> [!TIP]
> Wenn Sie das fertige Lernprogramm einfach herunterladen möchten, können Sie das GitHub- [Repository](https://github.com/microsoftgraph/msgraph-training-react-native)herunterladen oder Klonen.

## <a name="prerequisites"></a>Voraussetzungen

Bevor Sie mit diesem Lernprogramm beginnen, sollten Sie Folgendes auf Ihrem Entwicklungscomputer installiert haben.

- Mindestens eine der folgenden:
  - [Android Studio](https://developer.android.com/studio/) **und** [Java Development Kit](https://jdk.java.net) (erforderlich zum Ausführen des Beispiels unter Android)
  - [Xcode](https://developer.apple.com/xcode/) (erforderlich zum Ausführen des Beispiels unter IOS)
- [Node.js](https://nodejs.org)

Sie sollten auch über ein persönliches Microsoft-Konto mit einem Postfach auf Outlook.com oder ein Microsoft-Arbeits-oder Schulkonto verfügen. Wenn Sie kein Microsoft-Konto haben, gibt es mehrere Optionen, um ein kostenloses Konto zu erhalten:

- Sie können [sich für ein neues persönliches Microsoft-Konto registrieren](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).
- Sie können sich [für das Office 365 Entwicklerprogramm registrieren](https://developer.microsoft.com/office/dev-program) , um ein kostenloses Office 365-Abonnement zu erhalten.

> [!NOTE]
> Dieses Lernprogramm wurde mithilfe der nativen CLI-Reaktions Software geschrieben, die je nach Betriebssystem und Zielplattform spezifische Voraussetzungen hat. Anweisungen zum Konfigurieren des Entwicklungscomputers finden Sie unter [reagieren systemeigene erste Schritte](https://reactnative.dev/docs/environment-setup) . Die für dieses Lernprogramm verwendeten Versionen sind unten aufgeführt. Die Schritte in diesem Leitfaden funktionieren möglicherweise mit anderen Versionen, jedoch nicht getestet.
>
> - Android Studio Version 3.6.2 mit dem Android 9,0 SDK
> - Java Development Kit-Version 12.0.2
> - Xcode Version 11,4
> - Node. js-Version 12.16.2

## <a name="feedback"></a>Feedback

Geben Sie Feedback zu diesem Lernprogramm im [GitHub-Repository](https://github.com/microsoftgraph/msgraph-training-react-native)an.
