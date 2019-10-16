<!-- markdownlint-disable MD002 MD041 -->

In dieser Übung werden Sie das Microsoft Graph in die Anwendung integrieren. Für diese Anwendung verwenden Sie die [Microsoft Graph-JavaScript-Client Bibliothek](https://github.com/microsoftgraph/msgraph-sdk-javascript) , um Anrufe an Microsoft Graph vorzunehmen.

## <a name="get-calendar-events-from-outlook"></a>Abrufen von Kalenderereignissen aus Outlook

In diesem Abschnitt erweitern Sie die `GraphManager` Klasse so, dass eine Funktion hinzugefügt wird, um die Ereignisse `CalendarScreen` des Benutzers abzurufen und diese neuen Funktionen zu aktualisieren.

1. Öffnen Sie die Datei **GraphTutorial/Graph/graphmanager. js** , und fügen Sie der `GraphManager` Klasse die folgende Methode hinzu.

    ```js
    static getEvents = async() => {
      // GET /me/events
      return graphClient.api('/me/events')
        // $select='subject,organizer,start,end'
        // Only return these fields in results
        .select('subject,organizer,start,end')
        // $orderby=createdDateTime DESC
        // Sort results by when they were created, newest first
        .orderby('createdDateTime DESC')
        .get();
    }
    ```

    > [!NOTE]
    > Überprüfen Sie, was `getEvents` der Code in tut.
    >
    > - Die URL, die aufgerufen wird `/v1.0/me/events`.
    > - Die `select` Funktion schränkt die für die einzelnen Ereignisse zurückgegebenen Felder auf diejenigen ein, die von der APP tatsächlich verwendet werden.
    > - Die `orderby` -Funktion sortiert die Ergebnisse nach dem Datum und der Uhrzeit, zu der Sie erstellt wurden, wobei das letzte Element zuerst angezeigt wird.

1. Öffnen Sie die **GraphTutorial/views/CalendarScreen. js** , und ersetzen Sie den gesamten Inhalt durch den folgenden Code.

    ```JSX
    import React from 'react';
    import {
      ActivityIndicator,
      FlatList,
      Modal,
      ScrollView,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { Icon } from 'react-native-elements';
    import { GraphManager } from '../graph/GraphManager';

    export default class CalendarScreen extends React.Component {
      static navigationOptions = ({navigation}) => {
        return {
          title: 'Calendar',
          headerLeft: <Icon iconStyle={{ marginLeft: 10, color: 'white' }} size={30} name="menu" onPress={navigation.toggleDrawer} />
        };
      }

      state = {
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
          alert(error);
        }
      }

      // Temporary JSON view
      render() {
        return (
          <View style={styles.container}>
            <Modal visible={this.state.loadingEvents}>
              <View style={styles.loading}>
                <ActivityIndicator animating={this.state.loadingEvents} size='large' />
              </View>
            </Modal>
            <ScrollView>
              <Text>{JSON.stringify(this.state.events, null, 2)}</Text>
            </ScrollView>
          </View>
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

1. Öffnen Sie die Datei **GraphTutorial/Graph/graphmanager. js** , und fügen `import` Sie die folgende Anweisung am Anfang der Datei hinzu.

    ```js
    import moment from 'moment';
    ```

1. Fügen Sie die folgende **** Methode oberhalb `CalendarScreen` der Klassendeklaration hinzu.

    ```js
    convertDateTime = (dateTime) => {
      const utcTime = moment.utc(dateTime);
      return utcTime.local().format('MMM Do H:mm a');
    };
    ```

1. Ersetzen Sie `ScrollView` die in `render` der-Methode durch Folgendes.

    ```JSX
    <FlatList data={this.state.events}
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

    ![Ein Screenshot der Ereignistabelle](./images/calendar-list.png)
