# ICS-to-Google-Calendar
Simplifies adding ICS entries you get in Gmail to Google Calendar

I assume you know how to get to script.google.com and start a new project, and post the importEvents into the Code.gs tab and save it.  You will need to add in the Google Calendar service from the service tab before savings.  

To simplify use, you probably want to have Google drive mounted to your file system, on Win11, just download Google Drive Desktop.  You can then save ics to Gdrive.

This script is designed to import events from an ICS file into Google Calendar. Here's a step-by-step breakdown of the process:

1. **File Retrieval**:
    
    - The script looks for a file named "invite.ics" in Google Drive.
    - If the file is not found, it logs an error and stops.
    
2. **Content Extraction**:
    
    - The content of the ICS file is read and converted to a string.
    - If the file is empty, the script logs a message and stops.
    
3. **Calendar Identification**:
    
    - The script gets the ID of the default Google Calendar.
    
4. **Event Parsing**:
    
    - The `parseICalToEvents` function is called to convert the ICS content into event objects.
    - This function processes the ICS file line by line, extracting relevant information for each event.
    - It handles time zones, event start/end times, summaries, descriptions, and locations.
    
5. **Event Processing Loop**:
    
    - For each parsed event:  
        a. It checks if the event has both start and end times. If not, it skips the event.  
        b. It checks if the event already exists in the calendar using the `checkEventExists` function.  
        c. If the event doesn't exist, it inserts the new event into the calendar.
    
6. **Error Handling**:
    
    - The script uses try-catch blocks to handle errors during file reading and event insertion.
    - All actions and errors are logged for debugging purposes.
    
7. **Helper Functions**:
    
    - `formatDateTime`: Converts date-time strings from the ICS format to ISO 8601 format.
    - `convertToIANATimezone`: Maps Windows time zone names to IANA time zone identifiers.
    - `checkEventExists`: Checks if an event with the same summary and start time already exists in the calendar.
    

To use this script:

1. Ensure the "invite.ics" file is in your Google Drive.
2. Run the `importEvents` function from the Google Apps Script editor.
3. The script will process the file and add new events to your default Google Calendar.
4. Check the execution logs in the script editor for details on the import process.

So now that you have "importEvents" you have to be able to have it process automatically.

You could open the script editor every type and run the process, or you set up a trigger.  So you set a simple time based trigger:

So go to triggers, and:

Top box, pick importEvents
When it says which runs at head, it means it runs your latest version
Have it time-driven
Have an hour timer
Run every hour

Save this so you have a trigger running every hour

So basically, you get an email, you download the invitation as "invite.ics" to anywhere on google drive, and it will pick it up in an hour and post to your calendar.

If you are uncomfortable with the wait, you go to scripts.google.com and run it by pulling up the script and hitting the |> run button.  This will cause the invite to immediately be processed.

Then you should remove the ics.event off of google drive, which I've left as manual.  However you modify the script so it does it automatically.
