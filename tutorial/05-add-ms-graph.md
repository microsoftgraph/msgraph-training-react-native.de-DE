<!-- markdownlint-disable MD002 MD041 -->

In dieser Übung werden Sie das Microsoft Graph in die Anwendung integrieren. Für diese Anwendung verwenden Sie die [Microsoft Graph-JavaScript-Client Bibliothek](https://github.com/microsoftgraph/msgraph-sdk-javascript) , um Anrufe an Microsoft Graph vorzunehmen.

## <a name="get-calendar-events-from-outlook"></a>Abrufen von Kalenderereignissen von Outlook

In diesem Abschnitt erweitern Sie die `GraphManager` Klasse, um eine Funktion hinzuzufügen, um die Ereignisse des Benutzers für die aktuelle Woche abzurufen, und aktualisieren `CalendarScreen` , damit diese neuen Funktionen verwendet werden.

1. Öffnen Sie die Datei **GraphTutorial/Graph/graphmanager. TSX** , und fügen Sie der Klasse die folgende Methode hinzu `GraphManager` .

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="GetCalendarViewSnippet":::

    > [!NOTE]
    > Überprüfen Sie, was der Code in `getCalendarView` tut.
    >
    > - Die URL, die aufgerufen wird, lautet `/v1.0/me/calendarView`.
    > - Die `header` -Funktion fügt die `Prefer: outlook.timezone` Kopfzeile der Anforderung hinzu, wodurch sich die Zeiten in der Antwort in der bevorzugten Zeitzone des Benutzers befinden.
    > - Die `query` -Funktion fügt die `startDateTime` Parameter and hinzu und `endDateTime` definiert das Zeitfenster für die Kalenderansicht.
    > - Die `select` Funktion schränkt die für die einzelnen Ereignisse zurückgegebenen Felder auf diejenigen ein, die von der APP tatsächlich verwendet werden.
    > - Die `orderby` -Funktion sortiert die Ergebnisse nach dem Startzeitpunkt.
    > - Die `top` Funktion schränkt die Ergebnisse auf die ersten 50-Ereignisse ein.

1. Öffnen Sie die **GraphTutorial/views/CalendarScreen. TSX** , und ersetzen Sie den gesamten Inhalt durch den folgenden Code.

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

Sie können nun die app ausführen, sich anmelden und auf das Navigationselement **Kalender** im Menü tippen. Es sollte ein JSON-Dump der Ereignisse in der App angezeigt werden.

## <a name="display-the-results"></a>Anzeigen der Ergebnisse

Nun können Sie das JSON-Dump durch etwas ersetzen, um die Ergebnisse auf eine benutzerfreundliche Weise anzuzeigen. In diesem Abschnitt fügen Sie ein `FlatList` zum Bildschirm Kalender hinzu, um die Ereignisse zu rendern.

1. Fügen Sie die folgende Methode **oberhalb** der `CalendarScreen` Klassendeklaration hinzu.

    :::code language="typescript" source="../demo/GraphTutorial/screens/CalendarScreen.tsx" id="ConvertDateSnippet":::

1. Ersetzen Sie die `ScrollView` in der `CalendarComponent` -Methode durch Folgendes.

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

1. Führen Sie die APP aus, melden Sie sich an, und tippen Sie auf das Navigationselement **Kalender** . Die Liste der Ereignisse sollte angezeigt werden.

    ![Ein Screenshot der Tabelle mit Ereignissen](./images/calendar-list.png)
