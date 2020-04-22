<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="6db43-101">Beginnen Sie mit dem Erstellen eines neuen Reaktionssystem eigenen Projekts.</span><span class="sxs-lookup"><span data-stu-id="6db43-101">Begin by creating a new React Native project.</span></span>

1. <span data-ttu-id="6db43-102">Öffnen Sie die Befehlszeilenschnittstelle (CLI) in einem Verzeichnis, in dem Sie das Projekt erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="6db43-102">Open your command line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="6db43-103">Führen Sie den folgenden Befehl aus, um das [System "reagieresystem-CLI](https://github.com/facebook/react-native) " auszuführen und ein neues Reaktionssystem eigenes Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6db43-103">Run the following command to run the [react-native-cli](https://github.com/facebook/react-native) tool and create a new React Native project.</span></span>

    ```Shell
    npx react-native init GraphTutorial --template react-native-template-typescript
    ```

1. <span data-ttu-id="6db43-104">**Optional:** Stellen Sie sicher, dass die Entwicklungsumgebung ordnungsgemäß konfiguriert ist, indem Sie das Projekt durchführen.</span><span class="sxs-lookup"><span data-stu-id="6db43-104">**Optional:** Verify that your development environment is configured correctly by running the project.</span></span> <span data-ttu-id="6db43-105">Ändern Sie in ihrer CLI das Verzeichnis in das soeben erstellte **GraphTutorial** -Verzeichnis, und führen Sie einen der folgenden Befehle aus.</span><span class="sxs-lookup"><span data-stu-id="6db43-105">In your CLI, change the directory to the **GraphTutorial** directory you just created, and run one of the following commands.</span></span>

    - <span data-ttu-id="6db43-106">Für ios:`npx react-native run-ios`</span><span class="sxs-lookup"><span data-stu-id="6db43-106">For iOS: `npx react-native run-ios`</span></span>
    - <span data-ttu-id="6db43-107">Für Android: Starten Sie eine Android-Emulator-Instanz, und führen Sie`npx react-native run-android`</span><span class="sxs-lookup"><span data-stu-id="6db43-107">For Android: Launch an Android emulator instance and run `npx react-native run-android`</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="6db43-108">Installieren von Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="6db43-108">Install dependencies</span></span>

<span data-ttu-id="6db43-109">Installieren Sie vor dem Verschieben einige zusätzliche Abhängigkeiten, die Sie später verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="6db43-109">Before moving on, install some additional dependencies that you will use later.</span></span>

- <span data-ttu-id="6db43-110">[reagieren-Navigation](https://reactnavigation.org) zum Behandeln der Navigation zwischen Ansichten in der app.</span><span class="sxs-lookup"><span data-stu-id="6db43-110">[react-navigation](https://reactnavigation.org) to handle navigation between views in the app.</span></span>
- <span data-ttu-id="6db43-111">[reagieren – systemeigene gestenhandler](https://github.com/kmagiera/react-native-gesture-handler), [reagieren – systemeigene Sicherheit – Bereich – Kontext](https://github.com/th3rdwave/react-native-safe-area-context), [reagieren – systemeigene Bildschirme](https://github.com/kmagiera/react-native-screens), [reagieren – Native-Reanimierte](https://github.com/kmagiera/react-native-reanimated)und [maskierte Ansicht](https://github.com/react-native-community/react-native-masked-view) , erforderlich durch reagieren-Navigation.</span><span class="sxs-lookup"><span data-stu-id="6db43-111">[react-native-gesture-handler](https://github.com/kmagiera/react-native-gesture-handler), [react-native-safe-area-context](https://github.com/th3rdwave/react-native-safe-area-context), [react-native-screens](https://github.com/kmagiera/react-native-screens), [react-native-reanimate](https://github.com/kmagiera/react-native-reanimated), and [masked-view](https://github.com/react-native-community/react-native-masked-view) required by react-navigation.</span></span>
- <span data-ttu-id="6db43-112">[reagiere-Native-Elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) und [reagiere-Native-Vector-Icons](https://github.com/oblador/react-native-vector-icons) , um Symbole für die Benutzeroberfläche bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="6db43-112">[react-native-elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) and [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) to provide icons for the UI.</span></span>
- <span data-ttu-id="6db43-113">[reagiere-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) zur Behandlung von Authentifizierung und Tokenverwaltung.</span><span class="sxs-lookup"><span data-stu-id="6db43-113">[react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) to handle authentication and token management.</span></span>
- <span data-ttu-id="6db43-114">[Async-Storage](https://github.com/react-native-community/react-native-async-storage) zur Bereitstellung von Speicher für Token.</span><span class="sxs-lookup"><span data-stu-id="6db43-114">[async-storage](https://github.com/react-native-community/react-native-async-storage) to provide storage for tokens.</span></span>
- <span data-ttu-id="6db43-115">[Moment](https://momentjs.com) zum Analysieren und Vergleichen von Datums-und Uhrzeitangaben.</span><span class="sxs-lookup"><span data-stu-id="6db43-115">[moment](https://momentjs.com) to handle parsing and comparison of dates and times.</span></span>
- <span data-ttu-id="6db43-116">[Microsoft-Graph-Client](https://github.com/microsoftgraph/msgraph-sdk-javascript) zum tätigen von Anrufen an Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="6db43-116">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to the Microsoft Graph.</span></span>

1. <span data-ttu-id="6db43-117">Öffnen Sie die CLI im Stammverzeichnis Ihres Reaktionssystem eigenen Projekts.</span><span class="sxs-lookup"><span data-stu-id="6db43-117">Open your CLI in the root directory of your React Native project.</span></span>
1. <span data-ttu-id="6db43-118">Führen Sie den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="6db43-118">Run the following command.</span></span>

    ```Shell
    npm install @react-navigation/native@5.1.5 @react-navigation/drawer@5.4.1 @react-navigation/stack@5.2.10
    npm install @react-native-community/masked-view@0.1.7 react-native-safe-area-context@0.7.3
    npm install react-native-reanimated@1.8.0 react-native-screens@2.4.0 @react-native-community/async-storage@1.9.0
    npm install react-native-elements@1.2.7 react-native-vector-icons@6.6.0 react-native-gesture-handler@1.6.1
    npm install react-native-app-auth@5.1.1 moment@2.24.0 @microsoft/microsoft-graph-client@2.0.0
    ```

### <a name="link-and-configure-dependencies-for-ios"></a><span data-ttu-id="6db43-119">Verknüpfen und Konfigurieren von Abhängigkeiten für IOS</span><span class="sxs-lookup"><span data-stu-id="6db43-119">Link and configure dependencies for iOS</span></span>

> [!NOTE]
> <span data-ttu-id="6db43-120">Wenn Sie nicht auf IOS Zielen, können Sie diesen Abschnitt überspringen.</span><span class="sxs-lookup"><span data-stu-id="6db43-120">If you are not targeting iOS, you can skip this section.</span></span>

1. <span data-ttu-id="6db43-121">Öffnen Sie die CLI im **GraphTutorial/IOS-** Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="6db43-121">Open your CLI in the **GraphTutorial/ios** directory.</span></span>
1. <span data-ttu-id="6db43-122">Führen Sie den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="6db43-122">Run the following command.</span></span>

    ```Shell
    pod install
    ```

1. <span data-ttu-id="6db43-123">Öffnen Sie die Datei **GraphTutorial/IOS/GraphTutorial/Info. plist** in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="6db43-123">Open the **GraphTutorial/ios/GraphTutorial/Info.plist** file in a text editor.</span></span> <span data-ttu-id="6db43-124">Fügen Sie den folgenden kurz vor der `</dict>` letzten Textdatei hinzu.</span><span class="sxs-lookup"><span data-stu-id="6db43-124">Add the following just before the last `</dict>` line in the file.</span></span>

    ```xml
    <key>UIAppFonts</key>
    <array>
      <string>AntDesign.ttf</string>
      <string>Entypo.ttf</string>
      <string>EvilIcons.ttf</string>
      <string>Feather.ttf</string>
      <string>FontAwesome.ttf</string>
      <string>FontAwesome5_Brands.ttf</string>
      <string>FontAwesome5_Regular.ttf</string>
      <string>FontAwesome5_Solid.ttf</string>
      <string>Foundation.ttf</string>
      <string>Ionicons.ttf</string>
      <string>MaterialIcons.ttf</string>
      <string>MaterialCommunityIcons.ttf</string>
      <string>SimpleLineIcons.ttf</string>
      <string>Octicons.ttf</string>
      <string>Zocial.ttf</string>
    </array>
    ```

1. <span data-ttu-id="6db43-125">Öffnen Sie die Datei **GraphTutorial/IOS/GraphTutorial/AppDelegate. h** in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="6db43-125">Open the **GraphTutorial/ios/GraphTutorial/AppDelegate.h** file in a text editor.</span></span> <span data-ttu-id="6db43-126">Ersetzen Sie den Inhalt durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="6db43-126">Replace its contents with the following.</span></span>

    :::code language="objc" source="../demo/GraphTutorial/ios/GraphTutorial/AppDelegate.h":::

### <a name="configure-dependencies-for-android"></a><span data-ttu-id="6db43-127">Konfigurieren von Abhängigkeiten für Android</span><span class="sxs-lookup"><span data-stu-id="6db43-127">Configure dependencies for Android</span></span>

> [!NOTE]
> <span data-ttu-id="6db43-128">Wenn Sie nicht auf Android abzielen, können Sie diesen Abschnitt überspringen.</span><span class="sxs-lookup"><span data-stu-id="6db43-128">If you are not targeting Android, you can skip this section.</span></span>

1. <span data-ttu-id="6db43-129">Öffnen Sie die Datei **GraphTutorial/Android/App/Build. gradle** in einem Editor.</span><span class="sxs-lookup"><span data-stu-id="6db43-129">Open the **GraphTutorial/android/app/build.gradle** file in an editor.</span></span>
1. <span data-ttu-id="6db43-130">Suchen Sie `defaultConfig` den Eintrag, und fügen Sie die `defaultConfig`folgende Eigenschaft in hinzu.</span><span class="sxs-lookup"><span data-stu-id="6db43-130">Locate the `defaultConfig` entry and add the following property inside `defaultConfig`.</span></span>

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

    <span data-ttu-id="6db43-131">Der `defaultConfig` Eintrag sollte in etwa wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="6db43-131">The `defaultConfig` entry should look similar to the following.</span></span>

    :::code language="gradle" source="../demo/GraphTutorial/android/app/build.gradle" id="DefaultConfigSnippet":::

1. <span data-ttu-id="6db43-132">Fügen Sie am Ende der Datei die folgende Codezeile hinzu.</span><span class="sxs-lookup"><span data-stu-id="6db43-132">Add the following line to the end of the file.</span></span>

    ```Gradle
    apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
    ```

1. <span data-ttu-id="6db43-133">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="6db43-133">Save the file.</span></span>

## <a name="design-the-app"></a><span data-ttu-id="6db43-134">Entwerfen der App</span><span class="sxs-lookup"><span data-stu-id="6db43-134">Design the app</span></span>

<span data-ttu-id="6db43-135">Die Anwendung wird eine [Navigations Schublade](https://reactnavigation.org/docs/drawer-based-navigation.html) verwenden, um zwischen verschiedenen Ansichten zu navigieren.</span><span class="sxs-lookup"><span data-stu-id="6db43-135">The application will use a [navigation drawer](https://reactnavigation.org/docs/drawer-based-navigation.html) to navigate between different views.</span></span> <span data-ttu-id="6db43-136">In diesem Schritt werden Sie die grundlegenden Ansichten erstellen, die von der APP verwendet werden, und die Navigations Schublade implementieren.</span><span class="sxs-lookup"><span data-stu-id="6db43-136">In this step you will create the basic views used by the app and implement the navigation drawer.</span></span>

### <a name="create-views"></a><span data-ttu-id="6db43-137">Erstellen von Ansichten</span><span class="sxs-lookup"><span data-stu-id="6db43-137">Create views</span></span>

<span data-ttu-id="6db43-138">In diesem Abschnitt erstellen Sie die Ansichten für die APP zur Unterstützung eines [Authentifizierungs Flusses](https://reactnavigation.org/docs/auth-flow).</span><span class="sxs-lookup"><span data-stu-id="6db43-138">In this section you will create the views for the app to support an [authentication flow](https://reactnavigation.org/docs/auth-flow).</span></span>

1. <span data-ttu-id="6db43-139">Öffnen Sie **GraphTutorial/Index. js** , und fügen Sie das folgende oben in der Datei hinzu, bevor `import` Sie andere Anweisungen erhalten.</span><span class="sxs-lookup"><span data-stu-id="6db43-139">Open **GraphTutorial/index.js** and add the following to the top of the file, before any other `import` statements.</span></span>

    ```javascript
    import 'react-native-gesture-handler';
    ```

1. <span data-ttu-id="6db43-140">Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Dynpros**.</span><span class="sxs-lookup"><span data-stu-id="6db43-140">Create a new directory in the **GraphTutorial** directory named **screens**.</span></span>
1. <span data-ttu-id="6db43-141">Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/Screens** mit dem Namen **homescreen. TSX**.</span><span class="sxs-lookup"><span data-stu-id="6db43-141">Create a new file in the **GraphTutorial/screens** directory named **HomeScreen.tsx**.</span></span> <span data-ttu-id="6db43-142">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="6db43-142">Add the following code to the file.</span></span>

    ```typescript
    import React from 'react';
    import {
      ActivityIndicator,
      Alert,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';
    import { DrawerToggle, headerOptions } from '../menus/HeaderComponents';

    const Stack = createStackNavigator();
    const UserState = React.createContext({userLoading: true, userName: ''});

    type HomeScreenState = {
      userLoading: boolean;
      userName: string;
    }

    const HomeComponent = () => {
      const userState = React.useContext(UserState);

      return (
        <View style={styles.container}>
          <ActivityIndicator animating={userState.userLoading} size='large' />
          {userState.userLoading ? null: <Text>Hello {userState.userName}!</Text>}
        </View>
      );
    }

    export default class HomeScreen extends React.Component {

      state: HomeScreenState = {
        userLoading: true,
        userName: ''
      };

      render() {
        return (
          <UserState.Provider value={this.state}>
              <Stack.Navigator screenOptions={headerOptions}>
                <Stack.Screen name='Home'
                  component={HomeComponent}
                  options={{
                    title: 'Welcome',
                    headerLeft: () => <DrawerToggle/>
                  }} />
              </Stack.Navigator>
          </UserState.Provider>
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

1. <span data-ttu-id="6db43-143">Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/Screens** mit dem Namen **CalendarScreen. TSX**.</span><span class="sxs-lookup"><span data-stu-id="6db43-143">Create a new file in the **GraphTutorial/screens** directory named **CalendarScreen.tsx**.</span></span> <span data-ttu-id="6db43-144">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="6db43-144">Add the following code to the file.</span></span>

    ```typescript
    import React from 'react';
    import {
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';
    import { DrawerToggle, headerOptions } from '../menus/HeaderComponents';

    const Stack = createStackNavigator();

    // Temporary placeholder view
    const CalendarComponent = () => (
      <View style={styles.container}>
        <Text>Calendar</Text>
      </View>
    );

    export default class CalendarScreen extends React.Component {

      render() {
        return (
          <Stack.Navigator screenOptions={ headerOptions }>
            <Stack.Screen name='Calendar'
              component={ CalendarComponent }
              options={{
                title: 'Calendar',
                headerLeft: () => <DrawerToggle/>
              }} />
          </Stack.Navigator>
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

1. <span data-ttu-id="6db43-145">Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/Screens** mit dem Namen **SignInScreen. TSX**.</span><span class="sxs-lookup"><span data-stu-id="6db43-145">Create a new file in the **GraphTutorial/screens** directory named **SignInScreen.tsx**.</span></span> <span data-ttu-id="6db43-146">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="6db43-146">Add the following code to the file.</span></span>

    ```typescript
    // Adapted from https://reactnavigation.org/docs/auth-flow
    import React from 'react';
    import {
      Alert,
      Button,
      StyleSheet,
      View,
    } from 'react-native';
    import { NavigationContext } from '@react-navigation/native';

    export default class SignInScreen extends React.Component {
      static contextType = NavigationContext;

      static navigationOptions = {
        title: 'Please sign in',
      };

      _signInAsync = async () => {
        const navigation = this.context;

        // TEMPORARY
        navigation.reset({
          index: 0,
          routes: [ { name: 'Main' } ]
        });
      };

      render() {
        const navigation = this.context;
        navigation.setOptions({
          title: 'Please sign in',
          headerShown: true
        });

        return (
          <View style={styles.container}>
            <Button title='Sign In' onPress={this._signInAsync}/>
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

1. <span data-ttu-id="6db43-147">Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/Screens** mit dem Namen **AuthLoadingScreen. TSX**.</span><span class="sxs-lookup"><span data-stu-id="6db43-147">Create a new file in the **GraphTutorial/screens** directory named **AuthLoadingScreen.tsx**.</span></span> <span data-ttu-id="6db43-148">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="6db43-148">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/AuthLoadingScreen.tsx" id="AuthLoadingScreenSnippet":::

### <a name="create-a-navigation-drawer"></a><span data-ttu-id="6db43-149">Erstellen einer Navigations Schublade</span><span class="sxs-lookup"><span data-stu-id="6db43-149">Create a navigation drawer</span></span>

<span data-ttu-id="6db43-150">In diesem Abschnitt erstellen Sie ein Menü für die Anwendung und aktualisieren die Anwendung so, dass Sie zwischen den Bildschirmen mit der Option "reagieren-Navigation" wechselt.</span><span class="sxs-lookup"><span data-stu-id="6db43-150">In this section you will create a menu for the application, and update the application to use react-navigation to move between screens.</span></span>

1. <span data-ttu-id="6db43-151">Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Menüs**.</span><span class="sxs-lookup"><span data-stu-id="6db43-151">Create a new directory in the **GraphTutorial** directory named **menus**.</span></span>
1. <span data-ttu-id="6db43-152">Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/Menüs** mit dem Namen **HeaderComponents. TSX**.</span><span class="sxs-lookup"><span data-stu-id="6db43-152">Create a new file in the **GraphTutorial/menus** directory named **HeaderComponents.tsx**.</span></span> <span data-ttu-id="6db43-153">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="6db43-153">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/menus/HeaderComponents.tsx" id="HeaderComponentSnippet":::

1. <span data-ttu-id="6db43-154">Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/Menüs** mit dem Namen **DrawerMenu. TSX**.</span><span class="sxs-lookup"><span data-stu-id="6db43-154">Create a new file in the **GraphTutorial/menus** directory named **DrawerMenu.tsx**.</span></span> <span data-ttu-id="6db43-155">Fügen Sie den folgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="6db43-155">Add the following code to the file.</span></span>

    ```typescript
    import React, { FC } from 'react';
    import {
      Alert,
      Image,
      StyleSheet,
      Text,
      View,
      ImageSourcePropType
    } from 'react-native';
    import {
      createDrawerNavigator,
      DrawerContentScrollView,
      DrawerItem,
      DrawerItemList,
      DrawerContentComponentProps
    } from '@react-navigation/drawer';
    import { NavigationContext } from '@react-navigation/native';

    import HomeScreen from '../screens/HomeScreen';
    import CalendarScreen from '../screens/CalendarScreen';

    const Drawer = createDrawerNavigator();

    type CustomDrawerContentProps = DrawerContentComponentProps & {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
      signOut: () => void;
    }

    type DrawerMenuState = {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
    }

    const CustomDrawerContent: FC<CustomDrawerContentProps> = props => (
      <DrawerContentScrollView {...props}>
          <View style={styles.profileView}>
            <Image source={props.userPhoto}
              resizeMode='contain'
              style={styles.profilePhoto} />
            <Text style={styles.profileUserName}>{props.userName}</Text>
            <Text style={styles.profileEmail}>{props.userEmail}</Text>
          </View>
          <DrawerItemList {...props} />
          <DrawerItem label='Sign Out' onPress={props.signOut}/>
      </DrawerContentScrollView>
    );

    export default class DrawerMenuContent extends React.Component {
      static contextType = NavigationContext;

      state: DrawerMenuState = {
        // TEMPORARY
        userName: 'Adele Vance',
        userEmail: 'adelev@contoso.com',
        userPhoto: require('../images/no-profile-pic.png')
      }

      _signOut = async () => {
        const navigation = this.context;
        // Sign out
        // TEMPORARY
        navigation.reset({
          index: 0,
          routes: [{ name: 'SignIn' }]
        });
      }

      render() {
        const navigation = this.context;
        navigation.setOptions({
          headerShown: false,
        });

        return (
          <Drawer.Navigator
            drawerType='front'
            drawerContent={props => (
              <CustomDrawerContent {...props}
                userName={this.state.userName}
                userEmail={this.state.userEmail}
                userPhoto={this.state.userPhoto}
                signOut={this._signOut} />
            )}>
            <Drawer.Screen name='Home'
              component={HomeScreen}
              options={{drawerLabel: 'Home'}} />
            <Drawer.Screen name='Calendar'
              component={CalendarScreen}
              options={{drawerLabel: 'Calendar'}} />
          </Drawer.Navigator>
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

1. <span data-ttu-id="6db43-156">Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Images**.</span><span class="sxs-lookup"><span data-stu-id="6db43-156">Create a new directory in the **GraphTutorial** directory named **images**.</span></span>
1. <span data-ttu-id="6db43-157">Fügen Sie in diesem Verzeichnis ein Standardprofil Bild mit dem Namen " **No-Profile-PIC. png** " hinzu.</span><span class="sxs-lookup"><span data-stu-id="6db43-157">Add a default profile image named **no-profile-pic.png** in this directory.</span></span> <span data-ttu-id="6db43-158">Sie können ein beliebiges Bild verwenden oder [dieses in diesem Beispiel](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png)verwenden.</span><span class="sxs-lookup"><span data-stu-id="6db43-158">You can use any image you like, or use [the one from this sample](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png).</span></span>

1. <span data-ttu-id="6db43-159">Öffnen Sie die Datei **GraphTutorial/app. TSX** , und ersetzen Sie den gesamten Inhalt durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="6db43-159">Open the **GraphTutorial/App.tsx** file and replace the entire contents with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AppSnippet":::

1. <span data-ttu-id="6db43-160">Speichern Sie alle Änderungen.</span><span class="sxs-lookup"><span data-stu-id="6db43-160">Save all of your changes.</span></span>

1. <span data-ttu-id="6db43-161">Laden Sie die Anwendung in Ihrem Emulator neu.</span><span class="sxs-lookup"><span data-stu-id="6db43-161">Reload the application in your emulator.</span></span>

<span data-ttu-id="6db43-162">Das Menü der APP sollte zwischen den beiden Fragmenten navigieren und sich ändern, wenn Sie auf die Schaltflächen **Anmelden** oder **Abmelden** klicken.</span><span class="sxs-lookup"><span data-stu-id="6db43-162">The app's menu should work to navigate between the two fragments and change when you tap the **Sign in** or **Sign out** buttons.</span></span>

![Screenshots der Anwendung auf Android](./images/android-app-screens.png)

![Screenshots der Anwendung unter IOS](./images/ios-app-screens.png)
