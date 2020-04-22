<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="9513a-101">In dieser Übung werden Sie das Microsoft Graph in die Anwendung integrieren.</span><span class="sxs-lookup"><span data-stu-id="9513a-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="9513a-102">Für diese Anwendung verwenden Sie die [Microsoft Graph-JavaScript-Client Bibliothek](https://github.com/microsoftgraph/msgraph-sdk-javascript) , um Anrufe an Microsoft Graph vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="9513a-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="9513a-103">Abrufen von Kalenderereignissen von Outlook</span><span class="sxs-lookup"><span data-stu-id="9513a-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="9513a-104">In diesem Abschnitt erweitern Sie die `GraphManager` Klasse so, dass eine Funktion hinzugefügt wird, um die Ereignisse `CalendarScreen` des Benutzers abzurufen und diese neuen Funktionen zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="9513a-104">In this section you will extend the `GraphManager` class to add a function to get the user's events and update `CalendarScreen` to use these new functions.</span></span>

1. <span data-ttu-id="9513a-105">Öffnen Sie die Datei **GraphTutorial/Graph/graphmanager. TSX** , und fügen Sie der `GraphManager` Klasse die folgende Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="9513a-105">Open the **GraphTutorial/graph/GraphManager.tsx** file and add the following method to the `GraphManager` class.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="GetEventsSnippet":::

    > [!NOTE]
    > <span data-ttu-id="9513a-106">Überprüfen Sie, was `getEvents` der Code in tut.</span><span class="sxs-lookup"><span data-stu-id="9513a-106">Consider what the code in `getEvents` is doing.</span></span>
    >
    > - <span data-ttu-id="9513a-107">Die URL, die aufgerufen wird, lautet `/v1.0/me/events`.</span><span class="sxs-lookup"><span data-stu-id="9513a-107">The URL that will be called is `/v1.0/me/events`.</span></span>
    > - <span data-ttu-id="9513a-108">Die `select` Funktion schränkt die für die einzelnen Ereignisse zurückgegebenen Felder auf diejenigen ein, die von der APP tatsächlich verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="9513a-108">The `select` function limits the fields returned for each events to just those the app will actually use.</span></span>
    > - <span data-ttu-id="9513a-109">Die `orderby`-Funktion sortiert die Ergebnisse nach Datum und Uhrzeit ihrer Erstellung, wobei das aktuellste Element zuerst angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="9513a-109">The `orderby` function sorts the results by the date and time they were created, with the most recent item being first.</span></span>

1. <span data-ttu-id="9513a-110">Öffnen Sie die **GraphTutorial/views/CalendarScreen. TSX** , und ersetzen Sie den gesamten Inhalt durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="9513a-110">Open the **GraphTutorial/views/CalendarScreen.tsx** and replace its entire contents with the following code.</span></span>

    ```typescript
    import React from 'react';
    import {
      ActivityIndicator,
      Alert,
      FlatList,
      Modal,
      ScrollView,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';

    import { DrawerToggle, headerOptions } from '../menus/HeaderComponents';
    import { GraphManager } from '../graph/GraphManager';

    const Stack = createStackNavigator();
    const initialState: CalendarScreenState = { loadingEvents: true, events: []};
    const CalendarState = React.createContext(initialState);

    type CalendarScreenState = {
      loadingEvents: boolean;
      events: any[];
    }

    // Temporary JSON view
    const CalendarComponent = () => {
      const calendarState = React.useContext(CalendarState);

      return (
        <View style={styles.container}>
          <Modal visible={calendarState.loadingEvents}>
            <View style={styles.loading}>
              <ActivityIndicator animating={calendarState.loadingEvents} size='large' />
            </View>
          </Modal>
          <ScrollView>
            <Text>{JSON.stringify(calendarState.events, null, 2)}</Text>
          </ScrollView>
        </View>
      );
    }

    export default class CalendarScreen extends React.Component {

      state: CalendarScreenState = {
        loadingEvents: true,
        events: []
      };

      async componentDidMount() {
        try {
          const events = await GraphManager.getEvents();

          this.setState({
            loadingEvents: false,
            events: events.value
          });
        } catch(error) {
          Alert.alert(
            'Error getting events',
            JSON.stringify(error),
            [
              {
                text: 'OK'
              }
            ],
            { cancelable: false }
          );
        }
      }

      render() {
        return (
          <CalendarState.Provider value={this.state}>
            <Stack.Navigator screenOptions={ headerOptions }>
              <Stack.Screen name='Calendar'
                component={ CalendarComponent }
                options={{
                  title: 'Calendar',
                  headerLeft: () => <DrawerToggle/>
                }} />
            </Stack.Navigator>
          </CalendarState.Provider>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1
      },
      loading: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center'
      },
      eventItem: {
        padding: 10
      },
      eventSubject: {
        fontWeight: '700',
        fontSize: 18
      },
      eventOrganizer: {
        fontWeight: '200'
      },
      eventDuration: {
        fontWeight: '200'
      }
    });
    ```

<span data-ttu-id="9513a-111">Sie können nun die app ausführen, sich anmelden und auf das Navigationselement **Kalender** im Menü tippen.</span><span class="sxs-lookup"><span data-stu-id="9513a-111">You can now run the app, sign in, and tap the **Calendar** navigation item in the menu.</span></span> <span data-ttu-id="9513a-112">Es sollte ein JSON-Dump der Ereignisse in der App angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="9513a-112">You should see a JSON dump of the events in the app.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="9513a-113">Anzeigen der Ergebnisse</span><span class="sxs-lookup"><span data-stu-id="9513a-113">Display the results</span></span>

<span data-ttu-id="9513a-114">Nun können Sie das JSON-Dump durch etwas ersetzen, um die Ergebnisse auf eine benutzerfreundliche Weise anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="9513a-114">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="9513a-115">In diesem Abschnitt fügen Sie ein `FlatList` zum Bildschirm Kalender hinzu, um die Ereignisse zu rendern.</span><span class="sxs-lookup"><span data-stu-id="9513a-115">In this section, you will add a `FlatList` to the calendar screen to render the events.</span></span>

1. <span data-ttu-id="9513a-116">Öffnen Sie die Datei **GraphTutorial/Graph/Screens/CalendarScreen. TSX** , und `import` fügen Sie die folgende Anweisung am Anfang der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="9513a-116">Open the **GraphTutorial/graph/screens/CalendarScreen.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import moment from 'moment';
    ```

1. <span data-ttu-id="9513a-117">Fügen Sie die folgende **above** Methode oberhalb `CalendarScreen` der Klassendeklaration hinzu.</span><span class="sxs-lookup"><span data-stu-id="9513a-117">Add the following method **above** the `CalendarScreen` class declaration.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/CalendarScreen.tsx" id="ConvertDateSnippet":::

1. <span data-ttu-id="9513a-118">Ersetzen Sie `ScrollView` die in `CalendarComponent` der-Methode durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="9513a-118">Replace the `ScrollView` in the `CalendarComponent` method with the following.</span></span>

    ```typescript
    <FlatList data={calendarState.events}
      renderItem={({item}) =>
        <View style={styles.eventItem}>
          <Text style={styles.eventSubject}>{item.subject}</Text>
          <Text style={styles.eventOrganizer}>{item.organizer.emailAddress.name}</Text>
          <Text style={styles.eventDuration}>
            {convertDateTime(item.start.dateTime)} - {convertDateTime(item.end.dateTime)}
          </Text>
        </View>
      } />
    ```

1. <span data-ttu-id="9513a-119">Führen Sie die APP aus, melden Sie sich an, und tippen Sie auf das Navigationselement **Kalender** .</span><span class="sxs-lookup"><span data-stu-id="9513a-119">Run the app, sign in, and tap the **Calendar** navigation item.</span></span> <span data-ttu-id="9513a-120">Die Liste der Ereignisse sollte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="9513a-120">You should see the list of events.</span></span>

    ![Ein Screenshot der Tabelle mit Ereignissen](./images/calendar-list.png)
