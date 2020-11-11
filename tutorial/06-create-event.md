<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="f6ddd-101">In diesem Abschnitt können Sie die Möglichkeit zum Erstellen von Ereignissen im Kalender des Benutzers hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="f6ddd-101">In this section you will add the ability to create events on the user's calendar.</span></span>

## <a name="create-the-new-event-screen"></a><span data-ttu-id="f6ddd-102">Erstellen des neuen Ereignis Bildschirms</span><span class="sxs-lookup"><span data-stu-id="f6ddd-102">Create the new event screen</span></span>

1. <span data-ttu-id="f6ddd-103">Öffnen Sie **/Graph/GraphManager.TS** , und fügen Sie der-Klasse die folgende Funktion hinzu `GraphManager` .</span><span class="sxs-lookup"><span data-stu-id="f6ddd-103">Open **./graph/GraphManager.ts** and add the following function to the `GraphManager` class.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="CreateEventSnippet":::

    <span data-ttu-id="f6ddd-104">Diese Funktion verwendet das Graph-SDK, um ein neues Ereignis zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="f6ddd-104">This function uses the Graph SDK to create a new event.</span></span>

1. <span data-ttu-id="f6ddd-105">Erstellen Sie eine neue Datei im **./Screens** mit dem Namen **NewEventScreen. TSX** , und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="f6ddd-105">Create a new file in the **./screens** named **NewEventScreen.tsx** and add the following code.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/NewEventScreen.tsx" id="NewEventScreenSnippet":::

    <span data-ttu-id="f6ddd-106">Überprüfen Sie die Funktionsweise der `createEvent` Funktion.</span><span class="sxs-lookup"><span data-stu-id="f6ddd-106">Consider what the `createEvent` function does.</span></span> <span data-ttu-id="f6ddd-107">Es wird ein `MicrosoftGraph.Event` Objekt mithilfe der Werte aus dem Formular erstellt und übergibt dann dieses Objekt an die `GraphManager.createEvent` Funktion.</span><span class="sxs-lookup"><span data-stu-id="f6ddd-107">It creates a `MicrosoftGraph.Event` object using the values from the form, then passes that object to the `GraphManager.createEvent` function.</span></span>

1. <span data-ttu-id="f6ddd-108">Öffnen Sie **/Menus/DrawerMenu.TSX** , und fügen Sie die folgende `import` Anweisung am Anfang der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="f6ddd-108">Open **./menus/DrawerMenu.tsx** and add the following `import` statement at the top of the file.</span></span>

    ```typescript
    import NewEventScreen from '../screens/NewEventScreen';
    ```

1. <span data-ttu-id="f6ddd-109">Fügen Sie den folgenden Code innerhalb des `<Drawer.Navigator>` -Elements direkt oberhalb der `</Drawer.Navigator>` Linie hinzu.</span><span class="sxs-lookup"><span data-stu-id="f6ddd-109">Add the following code inside the `<Drawer.Navigator>` element, just above the `</Drawer.Navigator>` line.</span></span>

    ```typescript
    { userLoaded &&
      <Drawer.Screen name='NewEvent'
        component={NewEventScreen}
        options={{drawerLabel: 'New event'}} />
    }
    ```

1. <span data-ttu-id="f6ddd-110">Speichern Sie Ihre Änderungen, und starten oder aktualisieren Sie die APP neu.</span><span class="sxs-lookup"><span data-stu-id="f6ddd-110">Save your changes and restart or refresh the app.</span></span> <span data-ttu-id="f6ddd-111">Wählen Sie die Option **Neues Ereignis** im Menü aus, um zum neuen Ereignis Formular zu gelangen.</span><span class="sxs-lookup"><span data-stu-id="f6ddd-111">Select the **New event** option on the menu to get to the new event form.</span></span>

1. <span data-ttu-id="f6ddd-112">Füllen Sie das Formular aus, und wählen Sie **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="f6ddd-112">Fill in the form and select **Create**.</span></span>

    ![Screenshot des neuen Ereignis Formulars](images/new-event-form.png)
