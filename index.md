<html>

<head>
    <meta http-equiv="refresh" content="120">
    <meta http-equiv="cache-control" content="max-age=0" />
    <meta http-equiv="cache-control" content="no-cache" />
    <meta http-equiv="expires" content="0" />
    <meta http-equiv="expires" content="Tue, 01 Jan 1980 1:00:00 GMT" />
    <meta http-equiv="pragma" content="no-cache" />
</head>

<body>
    <script src="https://code.jquery.com/jquery-2.1.4.min.js"></script>
    <h1>HybridWebView Test</h1>
    <br /> Enter event name: <input type="text" id="name">
        <br /> Enter event id: <input type="text" id="eventId">
            <br /> Enter calendar id for event: <input type="text" id="eventCalendarId">
        <br /> Enter event description: <input type="text" id="eventDescription">
        <br /> Enter event start date ex:("Jan 1, 2021"): <input type="text" id="eventStartdate">
        <br /> Enter event end date ex:("Jan 1, 2021"): <input type="text" id="eventEnddate">
        <br />
    <br />
    <br /> Enter eventId for event to delete: <input type="text" id="eventId">
        <br />
    <br />
    <br /> Enter calendarId for events to list: <input type="text" id="calendarId">    
    <br />
    <br />
    <button type="button" onclick="javascript: addEvent($('#name').val(), $('#eventId').val(), $('#eventDescription').val(), $('#eventStartdate').val(), $('#eventEnddate').val(), $('#eventCalendarId').val())">Add event</button>
     <br />
    <br />
    <button type="button" onclick="javascript: deleteEvent($('#eventId').val())">Delete event</button>
    <button type="button" onclick="javascript: listEvents($('#calendarId').val())">List events for calender id</button>
    <br />
    <p id="result">Events:</p>
    <script type="text/javascript">
        function log(str) {
            $('#result').html($('#result').html() + "<br/>" + str);
        }

        log('Starting application')

        var selectedCalenderId = null;
        
        setTimeout(function() {
            CalendarIntegration.listCalendars();
        }, 100);

        function listCalendarsResult(result) {
            selectedCalenderId = result[0].id;
        
            log('Calendars loaded: ' + JSON.stringify(result))
        }        


        function addEvent(eventName, eventId, eventDescrip, eventStart, eventEnd, eventCalendarid) {
            CalendarIntegration.addEvent(eventCalendarid, eventId, eventName, eventDescrip, eventStart, eventEnd, "Timeplan");

            $('#name').val('');

            log('Event added to calendar');
        }
        
        function deleteEvent(eventId) {
            CalendarIntegration.deleteEvent(eventId);

            $('#eventId').val('');

            log('Event added to calendar');
        }        

        function listEvents(id) {
            CalendarIntegration.listEvents(id);
        }

        function listEventsResult(result) {
            log('Events in selected calendar (' + selectedCalenderId + '): ' + JSON.stringify(result));
        }

        function timeHasPassedEvent(time) {
            log('Event from app: ' + time);
        }
    </script>
</body>

</html>
