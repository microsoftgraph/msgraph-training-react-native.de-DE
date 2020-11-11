<!-- markdownlint-disable MD002 MD041 -->

Beginnen Sie mit dem Erstellen eines neuen Reaktionssystem eigenen Projekts.

1. Öffnen Sie die Befehlszeilenschnittstelle (CLI) in einem Verzeichnis, in dem Sie das Projekt erstellen möchten. Führen Sie den folgenden Befehl aus, um das [System "reagieresystem-CLI](https://github.com/facebook/react-native) " auszuführen und ein neues Reaktionssystem eigenes Projekt zu erstellen.

    ```Shell
    npx react-native init GraphTutorial --template react-native-template-typescript
    ```

1. **Optional:** Stellen Sie sicher, dass die Entwicklungsumgebung ordnungsgemäß konfiguriert ist, indem Sie das Projekt durchführen. Ändern Sie in ihrer CLI das Verzeichnis in das soeben erstellte **GraphTutorial** -Verzeichnis, und führen Sie einen der folgenden Befehle aus.

    - Für ios: `npx react-native run-ios`
    - Für Android: Starten Sie eine Android-Emulator-Instanz, und führen Sie `npx react-native run-android`

## <a name="install-dependencies"></a>Installieren von Abhängigkeiten

Installieren Sie vor dem Verschieben einige zusätzliche Abhängigkeiten, die Sie später verwenden werden.

- [reagieren-Navigation](https://reactnavigation.org) zum Behandeln der Navigation zwischen Ansichten in der app.
- [reagieren – systemeigene gestenhandler](https://github.com/kmagiera/react-native-gesture-handler), [reagieren – systemeigene Sicherheit – Bereich – Kontext](https://github.com/th3rdwave/react-native-safe-area-context), [reagieren – systemeigene Bildschirme](https://github.com/kmagiera/react-native-screens), [reagieren – Native-Reanimierte](https://github.com/kmagiera/react-native-reanimated)und [maskierte Ansicht](https://github.com/react-native-community/react-native-masked-view) , erforderlich durch reagieren-Navigation.
- [reagiere-Native-Elements](https://reactnativeelements.com/docs/) und [reagiere-Native-Vector-Icons](https://github.com/oblador/react-native-vector-icons) , um Symbole für die Benutzeroberfläche bereitzustellen.
- [reagiere-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) zur Behandlung von Authentifizierung und Tokenverwaltung.
- [Async-Storage](https://react-native-async-storage.github.io/async-storage/docs/install) zur Bereitstellung von Speicher für Token.
- [DateTimePicker](https://github.com/react-native-datetimepicker/datetimepicker) , um der Benutzeroberfläche Datums-und Zeitauswahl hinzuzufügen.
- [Moment](https://momentjs.com) zum Analysieren und Vergleichen von Datums-und Uhrzeitangaben.
- [Windows-IANA](https://github.com/rubenillodo/windows-iana) für die Übersetzung von Windows-Zeitzonen in das IANA-Format.
- [Microsoft-Graph-Client](https://github.com/microsoftgraph/msgraph-sdk-javascript) zum tätigen von Anrufen an Microsoft Graph.

1. Öffnen Sie die CLI im Stammverzeichnis Ihres Reaktionssystem eigenen Projekts.
1. Führen Sie den folgenden Befehl aus.

    ```Shell
    npm install @react-navigation/native@5.8.8 @react-navigation/drawer@5.11.1 @react-navigation/stack@5.12.5
    npm install @react-native-community/masked-view@0.1.10 react-native-safe-area-context@3.1.8 windows-iana
    npm install react-native-reanimated@1.13.1 react-native-screens@2.14.0 @react-native-async-storage/async-storage@1.13.2
    npm install react-native-elements@2.3.2 react-native-vector-icons@7.1.0 react-native-gesture-handler@1.8.0
    npm install react-native-app-auth@6.0.1 moment@2.29.1 moment-timezone @microsoft/microsoft-graph-client@2.1.1
    npm install @react-native-community/datetimepicker@3.0.4
    npm install @microsoft/microsoft-graph-types --save-dev
    ```

### <a name="link-and-configure-dependencies-for-ios"></a>Verknüpfen und Konfigurieren von Abhängigkeiten für IOS

> [!NOTE]
> Wenn Sie nicht auf IOS Zielen, können Sie diesen Abschnitt überspringen.

1. Öffnen Sie die CLI im **GraphTutorial/IOS-** Verzeichnis.
1. Führen Sie den folgenden Befehl aus.

    ```Shell
    pod install
    ```

1. Öffnen Sie die Datei **GraphTutorial/IOS/GraphTutorial/Info. plist** in einem Text-Editor. Fügen Sie den folgenden kurz vor der letzten `</dict>` Textdatei hinzu.

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

1. Öffnen Sie die Datei **GraphTutorial/IOS/GraphTutorial/AppDelegate. h** in einem Text-Editor. Ersetzen Sie den Inhalt durch Folgendes.

    :::code language="objc" source="../demo/GraphTutorial/ios/GraphTutorial/AppDelegate.h":::

### <a name="configure-dependencies-for-android"></a>Konfigurieren von Abhängigkeiten für Android

> [!NOTE]
> Wenn Sie nicht auf Android abzielen, können Sie diesen Abschnitt überspringen.

1. Öffnen Sie die Datei **GraphTutorial/Android/App/Build. gradle** in einem Editor.
1. Suchen `defaultConfig` Sie den Eintrag, und fügen Sie die folgende Eigenschaft in hinzu `defaultConfig` .

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

    Der `defaultConfig` Eintrag sollte in etwa wie folgt aussehen.

    :::code language="gradle" source="../demo/GraphTutorial/android/app/build.gradle" id="DefaultConfigSnippet":::

1. Fügen Sie am Ende der Datei die folgende Codezeile hinzu.

    ```Gradle
    apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
    ```

1. Speichern Sie die Datei.

## <a name="design-the-app"></a>Entwerfen der App

Die Anwendung wird eine [Navigations Schublade](https://reactnavigation.org/docs/drawer-based-navigation.html) verwenden, um zwischen verschiedenen Ansichten zu navigieren. In diesem Schritt werden Sie die grundlegenden Ansichten erstellen, die von der APP verwendet werden, und die Navigations Schublade implementieren.

### <a name="create-views"></a>Erstellen von Ansichten

In diesem Abschnitt erstellen Sie die Ansichten für die APP zur Unterstützung eines [Authentifizierungs Flusses](https://reactnavigation.org/docs/auth-flow).

1. Öffnen Sie **GraphTutorial/index.js** , und fügen Sie das folgende oben in der Datei hinzu, bevor Sie andere `import` Anweisungen erhalten.

    ```javascript
    import 'react-native-gesture-handler';
    ```

1. Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial** mit dem Namen **authcontext. TSX** , und fügen Sie den folgenden Code hinzu.

    :::code language="typescript" source="../demo/GraphTutorial/AuthContext.tsx" id="AuthContextSnippet":::

1. Erstellen Sie eine neue Datei im **GraphTutorial** -Verzeichnis mit dem Namen **userContext. TSX** , und fügen Sie den folgenden Code hinzu.

    :::code language="typescript" source="../demo/GraphTutorial/UserContext.tsx" id="UserContextSnippet":::

1. Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Dynpros**.
1. Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/Screens** mit dem Namen **homescreen. TSX**. Fügen Sie den folgenden Code in die Datei ein:

    :::code language="typescript" source="../demo/GraphTutorial/screens/HomeScreen.tsx" id="HomeScreenSnippet":::

1. Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/Screens** mit dem Namen **CalendarScreen. TSX**. Fügen Sie den folgenden Code in die Datei ein:

    ```typescript
    import React from 'react';
    import {
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';

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
          <Stack.Navigator>
            <Stack.Screen name='Calendar'
              component={ CalendarComponent }
              options={{
                headerShown: false
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

1. Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/Screens** mit dem Namen **SignInScreen. TSX**. Fügen Sie den folgenden Code in die Datei ein:

    ```typescript
    // Adapted from https://reactnavigation.org/docs/auth-flow
    import React from 'react';
    import {
      Alert,
      Button,
      StyleSheet,
      View,
    } from 'react-native';
    import { ParamListBase } from '@react-navigation/native';
    import { StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from '../AuthContext';

    type SignInProps = {
      navigation: StackNavigationProp<ParamListBase>;
    };

    export default class SignInScreen extends React.Component<SignInProps> {
      static contextType = AuthContext;

      _signInAsync = async () => {
        await this.context.signIn();
      };

      componentDidMount() {
        this.props.navigation.setOptions({
          title: 'Please sign in',
          headerShown: true
        });
      }

      render() {
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

1. Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/Screens** mit dem Namen **AuthLoadingScreen. TSX**. Fügen Sie den folgenden Code in die Datei ein:

    :::code language="typescript" source="../demo/GraphTutorial/screens/AuthLoadingScreen.tsx" id="AuthLoadingScreenSnippet":::

### <a name="create-a-navigation-drawer"></a>Erstellen einer Navigations Schublade

In diesem Abschnitt erstellen Sie ein Menü für die Anwendung und aktualisieren die Anwendung so, dass Sie zwischen den Bildschirmen mit der Option "reagieren-Navigation" wechselt.

1. Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Menüs**.

1. Erstellen Sie eine neue Datei im Verzeichnis **GraphTutorial/Menüs** mit dem Namen **DrawerMenu. TSX**. Fügen Sie den folgenden Code in die Datei ein:

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
    import { ParamListBase } from '@react-navigation/native';
    import { StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from '../AuthContext';
    import { UserContext } from '../UserContext';
    import HomeScreen from '../screens/HomeScreen';
    import CalendarScreen from '../screens/CalendarScreen';

    const Drawer = createDrawerNavigator();

    type CustomDrawerContentProps = DrawerContentComponentProps & {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
      signOut: () => void;
    }

    type DrawerMenuProps = {
      navigation: StackNavigationProp<ParamListBase>;
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

    export default class DrawerMenuContent extends React.Component<DrawerMenuProps> {
      static contextType = AuthContext;

      state = {
        // TEMPORARY
        userLoading: true,
        userFirstName: 'Adele',
        userFullName: 'Adele Vance',
        userEmail: 'adelev@contoso.com',
        userTimeZone: 'UTC',
        userPhoto: require('../images/no-profile-pic.png')
      }

      _signOut = async () => {
        this.context.signOut();
      }

      async componentDidMount() {
        this.props.navigation.setOptions({
          headerShown: false,
        });
      }

      render() {
        const userLoaded = !this.state.userLoading;

        return (
          <UserContext.Provider value={this.state}>
            <Drawer.Navigator
              drawerType='front'
              screenOptions={{
                headerStyle: {
                  backgroundColor: '#276b80'
                },
                headerTintColor: 'white'
              }}
              drawerContent={props => (
                <CustomDrawerContent {...props}
                  userName={this.state.userFullName}
                  userEmail={this.state.userEmail}
                  userPhoto={this.state.userPhoto}
                  signOut={this._signOut} />
              )}>
              <Drawer.Screen name='Home'
                component={HomeScreen}
                options={{drawerLabel: 'Home', headerTitle: 'Welcome'}} />
              { userLoaded &&
                <Drawer.Screen name='Calendar'
                  component={CalendarScreen}
                  options={{drawerLabel: 'Calendar'}} />
              }
            </Drawer.Navigator>
          </UserContext.Provider>
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

1. Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Images**.
1. Fügen Sie in diesem Verzeichnis ein Standardprofil Bild mit dem Namen **no-profile-pic.png** hinzu. Sie können ein beliebiges Bild verwenden oder [dieses in diesem Beispiel](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png)verwenden.

1. Öffnen Sie die Datei **GraphTutorial/app. TSX** , und ersetzen Sie den gesamten Inhalt durch Folgendes.

    ```typescript
    // Adapted from https://reactnavigation.org/docs/auth-flow
    import * as React from 'react';
    import { NavigationContainer, ParamListBase } from '@react-navigation/native';
    import { createStackNavigator, StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from './AuthContext';
    import SignInScreen from './screens/SignInScreen';
    import DrawerMenuContent from './menus/DrawerMenu'
    import AuthLoadingScreen from './screens/AuthLoadingScreen';

    const Stack = createStackNavigator();

    type Props = {
      navigation: StackNavigationProp<ParamListBase>;
    };

    export default function App({ navigation }: Props) {
      const [state, dispatch] = React.useReducer(
        (prevState: any, action: any) => {
          switch (action.type) {
            case 'RESTORE_TOKEN':
              return {
                ...prevState,
                userToken: action.token,
                isLoading: false
              };
            case 'SIGN_IN':
              return {
                ...prevState,
                isSignOut: false,
                userToken: action.token
              }
            case 'SIGN_OUT':
              return {
                ...prevState,
                isSignOut: true,
                userToken: null
              }
          }
        },
        {
          isLoading: true,
          isSignOut: false,
          userToken: null
        }
      );

      React.useEffect(() => {
        const bootstrapAsync = async () => {
          let userToken = null;
          // TEMPORARY
          dispatch({ type: 'RESTORE_TOKEN', token: userToken });
        };

        bootstrapAsync();
      }, []);

      const authContext = React.useMemo(
        () => ({
          signIn: async () => {
            dispatch({ type: 'SIGN_IN', token: 'placeholder-token' });
          },
          signOut: async () => {
            dispatch({ type: 'SIGN_OUT' });
          }
        }),
        []
      );

      return (
        <AuthContext.Provider value={authContext}>
          <NavigationContainer>
            <Stack.Navigator>
              {state.isLoading ? (
                <Stack.Screen name="Loading" component={AuthLoadingScreen} />
              ) : state.userToken == null ? (
                <Stack.Screen name="SignIn" component={SignInScreen} />
              ) : (
                <Stack.Screen name="Main" component={DrawerMenuContent} />
              )}
            </Stack.Navigator>
          </NavigationContainer>
        </AuthContext.Provider>
      );
    }
    ```

1. Speichern Sie alle Änderungen.

1. Laden Sie die Anwendung in Ihrem Emulator neu.

Das Menü der APP sollte zwischen den beiden Fragmenten navigieren und sich ändern, wenn Sie auf die Schaltflächen **Anmelden** oder **Abmelden** klicken.

![Screenshots der Anwendung auf Android](./images/android-app-screens.png)

![Screenshots der Anwendung unter IOS](./images/ios-app-screens.png)
