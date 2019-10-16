<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="66f8d-101">Beginnen Sie mit dem Erstellen eines neuen Reaktionssystem eigenen Projekts.</span><span class="sxs-lookup"><span data-stu-id="66f8d-101">Begin by creating a new React Native project.</span></span>

1. <span data-ttu-id="66f8d-102">Öffnen Sie die Befehlszeilenschnittstelle (CLI) in einem Verzeichnis, in dem Sie das Projekt erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="66f8d-102">Open your command line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="66f8d-103">Führen Sie den folgenden Befehl aus, um das [Reaktionssystem native-CLI-](https://github.com/facebook/react-native) Tool zu installieren und ein neues Reaktionssystem eigenes Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="66f8d-103">Run the following command to install the [react-native-cli](https://github.com/facebook/react-native) tool and create a new React Native project.</span></span>

    ```Shell
    npm install -g react-native-cli
    react-native init GraphTutorial
    ```

1. <span data-ttu-id="66f8d-104">**Optional:** Stellen Sie sicher, dass die Entwicklungsumgebung ordnungsgemäß konfiguriert ist, indem Sie das Projekt durchführen.</span><span class="sxs-lookup"><span data-stu-id="66f8d-104">**Optional:** Verify that your development environment is configured correctly by running the project.</span></span> <span data-ttu-id="66f8d-105">Ändern Sie in ihrer CLI das Verzeichnis in das soeben erstellte **GraphTutorial** -Verzeichnis, und führen Sie einen der folgenden Befehle aus.</span><span class="sxs-lookup"><span data-stu-id="66f8d-105">In your CLI, change the directory to the **GraphTutorial** directory you just created, and run one of the following commands.</span></span>

    - <span data-ttu-id="66f8d-106">Für ios:`react-native run-ios`</span><span class="sxs-lookup"><span data-stu-id="66f8d-106">For iOS: `react-native run-ios`</span></span>
    - <span data-ttu-id="66f8d-107">Für Android: Starten Sie eine Android-Emulator-Instanz, und führen Sie`react-native run-android`</span><span class="sxs-lookup"><span data-stu-id="66f8d-107">For Android: Launch an Android emulator instance and run `react-native run-android`</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="66f8d-108">Installieren von Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="66f8d-108">Install dependencies</span></span>

<span data-ttu-id="66f8d-109">Installieren Sie vor dem Verschieben einige zusätzliche Abhängigkeiten, die Sie später verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="66f8d-109">Before moving on, install some additional dependencies that you will use later.</span></span>

- <span data-ttu-id="66f8d-110">[reagieren-Navigation](https://reactnavigation.org) zum Behandeln der Navigation zwischen Ansichten in der app.</span><span class="sxs-lookup"><span data-stu-id="66f8d-110">[react-navigation](https://reactnavigation.org) to handle navigation between views in the app.</span></span>
- <span data-ttu-id="66f8d-111">[reagieren – systemeigene gestenhandler](https://github.com/kmagiera/react-native-gesture-handler) und [Reaktion – Native-reanimieren](https://github.com/kmagiera/react-native-reanimated), erforderlich durch reagieren-Navigation.</span><span class="sxs-lookup"><span data-stu-id="66f8d-111">[react-native-gesture-handler](https://github.com/kmagiera/react-native-gesture-handler) and [react-native-reanimate](https://github.com/kmagiera/react-native-reanimated), required by react-navigation.</span></span>
- <span data-ttu-id="66f8d-112">[reagiere-Native-Elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) und [reagiere-Native-Vector-Icons](https://github.com/oblador/react-native-vector-icons) , um Symbole für die Benutzeroberfläche bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="66f8d-112">[react-native-elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) and [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) to provide icons for the UI.</span></span>
- <span data-ttu-id="66f8d-113">[reagiere-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) zur Behandlung von Authentifizierung und Tokenverwaltung.</span><span class="sxs-lookup"><span data-stu-id="66f8d-113">[react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) to handle authentication and token management.</span></span>
- <span data-ttu-id="66f8d-114">[Moment](https://momentjs.com) zum Analysieren und Vergleichen von Datums-und Uhrzeitangaben.</span><span class="sxs-lookup"><span data-stu-id="66f8d-114">[moment](https://momentjs.com) to handle parsing and comparison of dates and times.</span></span>
- <span data-ttu-id="66f8d-115">[Microsoft-Graph-Client](https://github.com/microsoftgraph/msgraph-sdk-javascript) zum tätigen von Anrufen an Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="66f8d-115">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to the Microsoft Graph.</span></span>

1. <span data-ttu-id="66f8d-116">Öffnen Sie die CLI im Stammverzeichnis Ihres Reaktionssystem eigenen Projekts.</span><span class="sxs-lookup"><span data-stu-id="66f8d-116">Open your CLI in the root directory of your React Native project.</span></span>
1. <span data-ttu-id="66f8d-117">Führen Sie den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="66f8d-117">Run the following command.</span></span>

    ```Shell
    npm install react-navigation@3.11.1 react-native-gesture-handler@1.3.0 react-native-reanimated@1.1.0
    npm install react-native-elements@1.1.0 react-native-vector-icons@6.6.0 moment@2.24.0
    npm install react-native-app-auth@4.4.0 @microsoft/microsoft-graph-client@1.7.0
    react-native link react-native-vector-icons
    ```

### <a name="link-and-configure-dependencies-for-ios"></a><span data-ttu-id="66f8d-118">Verknüpfen und Konfigurieren von Abhängigkeiten für IOS</span><span class="sxs-lookup"><span data-stu-id="66f8d-118">Link and configure dependencies for iOS</span></span>

> [!NOTE]
> <span data-ttu-id="66f8d-119">Wenn Sie nicht auf IOS Zielen, können Sie diesen Abschnitt überspringen.</span><span class="sxs-lookup"><span data-stu-id="66f8d-119">If you are not targeting iOS, you can skip this section.</span></span>

1. <span data-ttu-id="66f8d-120">Öffnen Sie die CLI im **GraphTutorial/IOS-** Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="66f8d-120">Open your CLI in the **GraphTutorial/ios** directory.</span></span>
1. <span data-ttu-id="66f8d-121">Führen Sie den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="66f8d-121">Run the following command.</span></span>

    ```Shell
    pod install
    ```

1. <span data-ttu-id="66f8d-122">Öffnen Sie die Datei **GraphTutorial/IOS/GraphTutorial/AppDelegate. h** in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="66f8d-122">Open the **GraphTutorial/ios/GraphTutorial/AppDelegate.h** file in a text editor.</span></span> <span data-ttu-id="66f8d-123">Ersetzen Sie den Inhalt durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="66f8d-123">Replace its contents with the following.</span></span>

    ```obj-c
    #import <React/RCTBridgeDelegate.h>
    #import <UIKit/UIKit.h>
    #import "RNAppAuthAuthorizationFlowManager.h"

    @interface AppDelegate : UIResponder <UIApplicationDelegate, RCTBridgeDelegate, RNAppAuthAuthorizationFlowManager>

    @property (nonatomic, strong) UIWindow *window;
    @property (nonatomic, weak) id<RNAppAuthAuthorizationFlowManagerDelegate> authorizationFlowManagerDelegate;

    @end
    ```

### <a name="configure-dependencies-for-android"></a><span data-ttu-id="66f8d-124">Konfigurieren von Abhängigkeiten für Android</span><span class="sxs-lookup"><span data-stu-id="66f8d-124">Configure dependencies for Android</span></span>

> [!NOTE]
> <span data-ttu-id="66f8d-125">Wenn Sie nicht auf Android abzielen, können Sie diesen Abschnitt überspringen.</span><span class="sxs-lookup"><span data-stu-id="66f8d-125">If you are not targeting Android, you can skip this section.</span></span>

1. <span data-ttu-id="66f8d-126">Öffnen Sie die Datei **GraphTutorial/Android/App/Build. gradle** in einem Editor.</span><span class="sxs-lookup"><span data-stu-id="66f8d-126">Open the **GraphTutorial/android/app/build.gradle** file in an editor.</span></span>
1. <span data-ttu-id="66f8d-127">Suchen Sie `defaultConfig` den Eintrag, und fügen Sie die `defaultConfig`folgende Eigenschaft in hinzu.</span><span class="sxs-lookup"><span data-stu-id="66f8d-127">Locate the `defaultConfig` entry and add the following property inside `defaultConfig`.</span></span>

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

1. <span data-ttu-id="66f8d-128">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="66f8d-128">Save the file.</span></span> <span data-ttu-id="66f8d-129">Der `defaultConfig` Eintrag sollte in etwa wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="66f8d-129">The `defaultConfig` entry should look similar to the following.</span></span>

    ```Gradle
    defaultConfig {
        applicationId "com.graphtutorial"
        minSdkVersion rootProject.ext.minSdkVersion
        targetSdkVersion rootProject.ext.targetSdkVersion
        versionCode 1
        versionName "1.0"
        manifestPlaceholders = [
            appAuthRedirectScheme: 'graphtutorial'
        ]
    }
    ```

## <a name="design-the-app"></a><span data-ttu-id="66f8d-130">Entwerfen der APP</span><span class="sxs-lookup"><span data-stu-id="66f8d-130">Design the app</span></span>

<span data-ttu-id="66f8d-131">Die Anwendung wird eine [Navigations Schublade](https://reactnavigation.org/docs/drawer-based-navigation.html) verwenden, um zwischen verschiedenen Ansichten zu navigieren.</span><span class="sxs-lookup"><span data-stu-id="66f8d-131">The application will use a [navigation drawer](https://reactnavigation.org/docs/drawer-based-navigation.html) to navigate between different views.</span></span> <span data-ttu-id="66f8d-132">In diesem Schritt werden Sie die grundlegenden Ansichten erstellen, die von der APP verwendet werden, und die Navigations Schublade implementieren.</span><span class="sxs-lookup"><span data-stu-id="66f8d-132">In this step you will create the basic views used by the app and implement the navigation drawer.</span></span>

### <a name="create-views"></a><span data-ttu-id="66f8d-133">Erstellen von Ansichten</span><span class="sxs-lookup"><span data-stu-id="66f8d-133">Create views</span></span>

<span data-ttu-id="66f8d-134">In diesem Abschnitt erstellen Sie die Ansichten für die APP zur Unterstützung eines [Authentifizierungs Flusses](https://reactnavigation.org/docs/auth-flow.html).</span><span class="sxs-lookup"><span data-stu-id="66f8d-134">In this section you will create the views for the app to support an [authentication flow](https://reactnavigation.org/docs/auth-flow.html).</span></span>

1. <span data-ttu-id="66f8d-135">Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **views**.</span><span class="sxs-lookup"><span data-stu-id="66f8d-135">Create a new directory in the **GraphTutorial** directory named **views**.</span></span>
1. <span data-ttu-id="66f8d-136">Erstellen Sie eine neue Datei im **GraphTutorial/views-** Verzeichnis mit dem Namen **homescreen. js**.</span><span class="sxs-lookup"><span data-stu-id="66f8d-136">Create a new file in the **GraphTutorial/views** directory named **HomeScreen.js**.</span></span> <span data-ttu-id="66f8d-137">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="66f8d-137">Add the following code to the file.</span></span>

    ```JSX
    import React from 'react';
    import {
      ActivityIndicator,
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { Icon } from 'react-native-elements';

    export default class HomeScreen extends React.Component {
      static navigationOptions = ({navigation}) => {
        return {
          title: 'Welcome',
          headerLeft: <Icon iconStyle={{ marginLeft: 10, color: 'white' }} size={30} name="menu" onPress={navigation.toggleDrawer} />
        };
      }

      state = {
        userLoading: true,
        userName: ''
      };

      render() {
        return (
          <View style={styles.container}>
            <ActivityIndicator animating={this.state.userLoading} size='large' />
            {this.state.userLoading ? null: <Text>Hello {this.state.userName}!</Text>}
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      }
    });
    ```

1. <span data-ttu-id="66f8d-138">Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/views** mit dem Namen **CalendarScreen. js**.</span><span class="sxs-lookup"><span data-stu-id="66f8d-138">Create a new file in the **GraphTutorial/views** directory named **CalendarScreen.js**.</span></span> <span data-ttu-id="66f8d-139">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="66f8d-139">Add the following code to the file.</span></span>

    ```JSX
    import React from 'react';
    import {
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { Icon } from 'react-native-elements';

    export default class CalendarScreen extends React.Component {
      static navigationOptions = ({navigation}) => {
        return {
          title: 'Calendar',
          headerLeft: <Icon iconStyle={{ marginLeft: 10, color: 'white' }} size={30} name="menu" onPress={navigation.toggleDrawer} />
        };
      }

      // Temporary placeholder view
      render() {
        return (
          <View style={styles.container}>
            <Text>Calendar</Text>
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      }
    });
    ```

1. <span data-ttu-id="66f8d-140">Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/views** mit dem Namen **SignInScreen. js**.</span><span class="sxs-lookup"><span data-stu-id="66f8d-140">Create a new file in the **GraphTutorial/views** directory named **SignInScreen.js**.</span></span> <span data-ttu-id="66f8d-141">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="66f8d-141">Add the following code to the file.</span></span>

    ```JSX
    // Adapted from https://reactnavigation.org/docs/auth-flow.html
    import React from 'react';
    import {
      Button,
      StyleSheet,
      View,
    } from 'react-native';

    export default class SignInScreen extends React.Component {
      static navigationOptions = {
        title: 'Please sign in',
      };

      _signInAsync = async () => {
        // TEMPORARY
        this.props.navigation.navigate('App');
      };

      render() {
        return (
          <View style={styles.container}>
            <Button title="Sign In" onPress={this._signInAsync}/>
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      }
    });
    ```

1. <span data-ttu-id="66f8d-142">Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/views** mit dem Namen **AuthLoadingScreen. js**.</span><span class="sxs-lookup"><span data-stu-id="66f8d-142">Create a new file in the **GraphTutorial/views** directory named **AuthLoadingScreen.js**.</span></span> <span data-ttu-id="66f8d-143">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="66f8d-143">Add the following code to the file.</span></span>

    ```JSX
    // Adapted from https://reactnavigation.org/docs/auth-flow.html
    import React from 'react';
    import {
      ActivityIndicator,
      AsyncStorage,
      Text,
      StyleSheet,
      View,
    } from 'react-native';

    export default class AuthLoadingScreen extends React.Component {

      componentDidMount() {
        this._bootstrapAsync();
      }

      // Fetch the token from storage then navigate to our appropriate place
      // NOTE: Production apps should protect user tokens in secure storage.
      _bootstrapAsync = async () => {
        const userToken = await AsyncStorage.getItem('userToken');

        // This will switch to the App screen or Auth screen and this loading
        // screen will be unmounted and thrown away.
        this.props.navigation.navigate(userToken ? 'App' : 'Auth');
      };

      render() {
        return (
          <View style={styles.container}>
            <ActivityIndicator size='large' />
            <Text style={styles.statusText}>Logging in...</Text>
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      },
      statusText: {
        marginTop: 10
      }
    });
    ```

### <a name="create-a-navigation-drawer"></a><span data-ttu-id="66f8d-144">Erstellen einer Navigations Schublade</span><span class="sxs-lookup"><span data-stu-id="66f8d-144">Create a navigation drawer</span></span>

<span data-ttu-id="66f8d-145">In diesem Abschnitt erstellen Sie ein Menü für die Anwendung und aktualisieren die Anwendung so, dass Sie zwischen den Bildschirmen mit der Option "reagieren-Navigation" wechselt.</span><span class="sxs-lookup"><span data-stu-id="66f8d-145">In this section you will create a menu for the application, and update the application to use react-navigation to move between screens.</span></span>

1. <span data-ttu-id="66f8d-146">Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Menüs**.</span><span class="sxs-lookup"><span data-stu-id="66f8d-146">Create a new directory in the **GraphTutorial** directory named **menus**.</span></span>
1. <span data-ttu-id="66f8d-147">Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/Menüs** mit dem Namen **DrawerMenu. js**.</span><span class="sxs-lookup"><span data-stu-id="66f8d-147">Create a new file in the **GraphTutorial/menus** directory named **DrawerMenu.js**.</span></span> <span data-ttu-id="66f8d-148">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="66f8d-148">Add the following code to the file.</span></span>

    ```JSX
    import React from 'react';
    import {
      Image,
      SafeAreaView,
      ScrollView,
      StyleSheet,
      Text,
      View
    } from 'react-native';
    import { DrawerItems } from 'react-navigation';

    export default class DrawerMenuContent extends React.Component {

      state = {
        // TEMPORARY
        userName: 'Adele Vance',
        userEmail: 'adelev@contoso.com',
        userPhoto: require('../images/no-profile-pic.png')
      }

      // Check if user tapped on the Sign Out button and
      // sign the user out
      _onItemPressed = async (route) => {
        if (route.route.routeName !== 'Sign Out') {
          this.props.onItemPress(route);
          return;
        }

        // Sign out
        // TEMPORARY
        this.props.navigation.navigate('Auth');
      }

      render() {
        return (
          <ScrollView>
            <SafeAreaView style={styles.container}
              forceInset={{ top: 'always', horizontal: 'never' }}>
              <View style={styles.profileView}>
                <Image source={this.state.userPhoto}
                  resizeMode='contain'
                  style={styles.profilePhoto} />
                <Text style={styles.profileUserName}>{this.state.userName}</Text>
                <Text style={styles.profileEmail}>{this.state.userEmail}</Text>
              </View>
              <DrawerItems {...this.props}
                onItemPress={this._onItemPressed}/>
            </SafeAreaView>
          </ScrollView>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1
      },
      profileView: {
        alignItems: 'center',
        padding: 10
      },
      profilePhoto: {
        width: 80,
        height: 80,
        borderRadius: 40
      },
      profileUserName: {
        fontWeight: '700'
      },
      profileEmail: {
        fontWeight: '200',
        fontSize: 10
      }
    });
    ```

1. <span data-ttu-id="66f8d-149">Öffnen Sie die Datei **GraphTutorial/app. js** , und ersetzen Sie den gesamten Inhalt durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="66f8d-149">Open the **GraphTutorial/App.js** file and replace the entire contents with the following.</span></span>

    ```JSX
    // Adapted from https://reactnavigation.org/docs/auth-flow.html
    import {
      createSwitchNavigator,
      createStackNavigator,
      createDrawerNavigator,
      createAppContainer } from "react-navigation";

    import AuthLoadingScreen from './views/AuthLoadingScreen';
    import SignInScreen from './views/SignInScreen';
    import HomeScreen from './views/HomeScreen';
    import CalendarScreen from './views/CalendarScreen';
    import DrawerMenuContent from './menus/DrawerMenu';

    const headerOptions = {
      defaultNavigationOptions: {
        headerStyle: {
          backgroundColor: '#276b80'
        },
        headerTintColor: 'white'
      }
    };

    const AuthStack = createStackNavigator(
      {
        SignIn: SignInScreen
      },
      headerOptions
    );

    const AppDrawer = createDrawerNavigator(
      {
        Home: createStackNavigator({ Home: HomeScreen }, headerOptions),
        Calendar: createStackNavigator({ Calendar: CalendarScreen }, headerOptions),
        'Sign Out': 'SignOut'
      },
      {
        hideStatusBar: false,
        contentComponent: DrawerMenuContent
      }
    );

    export default createAppContainer(createSwitchNavigator(
      {
        AuthLoading: AuthLoadingScreen,
        App: AppDrawer,
        Auth: AuthStack
      },
      {
        initialRouteName: 'AuthLoading'
      }
    ));

1. Save all of your changes.

1. Reload the application in your emulator.

The app's menu should work to navigate between the two fragments and change when you tap the **Sign in** or **Sign out** buttons.

![Screenshots of the application on Android](./images/android-app-screens.png)

![Screenshots of the application on iOS](./images/ios-app-screens.png)

> [!NOTE]
> You may receive warnings when running the app about Async Storage or componentWillUpdate. For the purposes of this tutorial, you can dismiss those warnings.
