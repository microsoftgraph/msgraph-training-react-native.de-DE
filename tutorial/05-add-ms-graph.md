<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="8c509-101">In dieser Übung werden Sie das Microsoft Graph in die Anwendung integrieren.</span><span class="sxs-lookup"><span data-stu-id="8c509-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="8c509-102">Für diese Anwendung verwenden Sie die [Microsoft Graph-JavaScript-Client Bibliothek](https://github.com/microsoftgraph/msgraph-sdk-javascript) , um Anrufe an Microsoft Graph vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="8c509-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="8c509-103">Abrufen von Kalenderereignissen von Outlook</span><span class="sxs-lookup"><span data-stu-id="8c509-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="8c509-104">In diesem Abschnitt erweitern Sie die `GraphManager` Klasse, um eine Funktion hinzuzufügen, um die Ereignisse des Benutzers für die aktuelle Woche abzurufen, und aktualisieren `CalendarScreen` , damit diese neuen Funktionen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="8c509-104">In this section you will extend the `GraphManager` class to add a function to get the user's events for the current week and update `CalendarScreen` to use these new functions.</span></span>

1. <span data-ttu-id="8c509-105">Öffnen Sie die Datei **GraphTutorial/Graph/graphmanager. TSX** , und fügen Sie der Klasse die folgende Methode hinzu `GraphManager` .</span><span class="sxs-lookup"><span data-stu-id="8c509-105">Open the **GraphTutorial/graph/GraphManager.tsx** file and add the following method to the `GraphManager` class.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="GetCalendarViewSnippet":::

    > [!NOTE]
    > <span data-ttu-id="8c509-106">Überprüfen Sie, was der Code in `getCalendarView` tut.</span><span class="sxs-lookup"><span data-stu-id="8c509-106">Consider what the code in `getCalendarView` is doing.</span></span>
    >
    > - <span data-ttu-id="8c509-107">Die URL, die aufgerufen wird, lautet `/v1.0/me/calendarView`.</span><span class="sxs-lookup"><span data-stu-id="8c509-107">The URL that will be called is `/v1.0/me/calendarView`.</span></span>
    > - <span data-ttu-id="8c509-108">Die `header` -Funktion fügt die `Prefer: outlook.timezone` Kopfzeile der Anforderung hinzu, wodurch sich die Zeiten in der Antwort in der bevorzugten Zeitzone des Benutzers befinden.</span><span class="sxs-lookup"><span data-stu-id="8c509-108">The `header` function adds the `Prefer: outlook.timezone` header to the request, causing the times in the response to be in the user's preferred time zone.</span></span>
    > - <span data-ttu-id="8c509-109">Die `query` -Funktion fügt die `startDateTime` Parameter and hinzu und `endDateTime` definiert das Zeitfenster für die Kalenderansicht.</span><span class="sxs-lookup"><span data-stu-id="8c509-109">The `query` function adds the `startDateTime` and `endDateTime` parameters, defining the window of time for the calendar view.</span></span>
    > - <span data-ttu-id="8c509-110">Die `select` Funktion schränkt die für die einzelnen Ereignisse zurückgegebenen Felder auf diejenigen ein, die von der APP tatsächlich verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="8c509-110">The `select` function limits the fields returned for each events to just those the app will actually use.</span></span>
    > - <span data-ttu-id="8c509-111">Die `orderby` -Funktion sortiert die Ergebnisse nach dem Startzeitpunkt.</span><span class="sxs-lookup"><span data-stu-id="8c509-111">The `orderby` function sorts the results by the start time.</span></span>
    > - <span data-ttu-id="8c509-112">Die `top` Funktion schränkt die Ergebnisse auf die ersten 50-Ereignisse ein.</span><span class="sxs-lookup"><span data-stu-id="8c509-112">The `top` function limits the results to the first 50 events.</span></span>

1. <span data-ttu-id="8c509-113">Öffnen Sie die **GraphTutorial/views/CalendarScreen. TSX** , und ersetzen Sie den gesamten Inhalt durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="8c509-113">Open the **GraphTutorial/views/CalendarScreen.tsx** and replace its entire contents with the following code.</span></span>

    ```typescript
    import React from 'react';
    import {
      ActivityIndicator,
      Alert,
      FlatList,
      Modal,
      Platform,
      ScrollView,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    import moment from 'moment-timezone';
    import { findOneIana } from 'windows-iana';

    import { UserContext } from '../UserContext';
    import { GraphManager } from '../graph/GraphManager';

    const Stack = createStackNavigator();
    const CalendarState = React.createContext<CalendarScreenState>({
      loadingEvents: true,
      events: []
    });

    type CalendarScreenState = {
      loadingEvents: boolean;
      events: MicrosoftGraph.Event[];
    }

    // Temporary JSON view
    const CalendarComponent = () => {
      const calendarState = React.useContext(CalendarState);

      return (
        <View style={styles.container}>
          <Modal visible={calendarState.loadingEvents}>
            <View style={styles.loading}>
              <ActivityIndicator
                color={Platform.OS === 'android' ? '#276b80' : undefined}
                animating={calendarState.loadingEvents}
                size='large' />
            </View>
          </Modal>
          <ScrollView>
            <Text>{JSON.stringify(calendarState.events, null, 2)}</Text>
          </ScrollView>
        </View>
      );
    }

    export default class CalendarScreen extends React.Component {
      static contextType = UserContext;

      state: CalendarScreenState = {
        loadingEvents: true,
        events: []
      };

      async componentDidMount() {
        try {
          const tz = this.context.userTimeZone || 'UTC';
          // Convert user's Windows time zone ("Pacific Standard Time")
          // to IANA format ("America/Los_Angeles")
          // Moment.js needs IANA format
          const ianaTimeZone = findOneIana(tz);

          // Get midnight on the start of the current week in the user's
          // time zone, but in UTC. For example, for PST, the time value
          // would be 07:00:00Z
          const startOfWeek = moment
            .tz(ianaTimeZone!.valueOf())
            .startOf('week')
            .utc();

          const endOfWeek = moment(startOfWeek)
            .add(7, 'day');

          const events = await GraphManager.getCalendarView(
            startOfWeek.format(),
            endOfWeek.format(),
            tz);

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
            <Stack.Navigator>
              <Stack.Screen name='Calendar'
                component={ CalendarComponent }
                options={{
                  headerShown: false
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

<span data-ttu-id="8c509-114">Sie können nun die app ausführen, sich anmelden und auf das Navigationselement **Kalender** im Menü tippen.</span><span class="sxs-lookup"><span data-stu-id="8c509-114">You can now run the app, sign in, and tap the **Calendar** navigation item in the menu.</span></span> <span data-ttu-id="8c509-115">Es sollte ein JSON-Dump der Ereignisse in der App angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="8c509-115">You should see a JSON dump of the events in the app.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="8c509-116">Anzeigen der Ergebnisse</span><span class="sxs-lookup"><span data-stu-id="8c509-116">Display the results</span></span>

<span data-ttu-id="8c509-117">Nun können Sie das JSON-Dump durch etwas ersetzen, um die Ergebnisse auf eine benutzerfreundliche Weise anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="8c509-117">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="8c509-118">In diesem Abschnitt fügen Sie ein `FlatList` zum Bildschirm Kalender hinzu, um die Ereignisse zu rendern.</span><span class="sxs-lookup"><span data-stu-id="8c509-118">In this section, you will add a `FlatList` to the calendar screen to render the events.</span></span>

1. <span data-ttu-id="8c509-119">Fügen Sie die folgende Methode **oberhalb** der `CalendarScreen` Klassendeklaration hinzu.</span><span class="sxs-lookup"><span data-stu-id="8c509-119">Add the following method **above** the `CalendarScreen` class declaration.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/CalendarScreen.tsx" id="ConvertDateSnippet":::

1. <span data-ttu-id="8c509-120">Ersetzen Sie die `ScrollView` in der `CalendarComponent` -Methode durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="8c509-120">Replace the `ScrollView` in the `CalendarComponent` method with the following.</span></span>

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

1. <span data-ttu-id="8c509-121">Führen Sie die APP aus, melden Sie sich an, und tippen Sie auf das Navigationselement **Kalender** .</span><span class="sxs-lookup"><span data-stu-id="8c509-121">Run the app, sign in, and tap the **Calendar** navigation item.</span></span> <span data-ttu-id="8c509-122">Die Liste der Ereignisse sollte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="8c509-122">You should see the list of events.</span></span>

    ![Ein Screenshot der Tabelle mit Ereignissen](./images/calendar-list.png)
