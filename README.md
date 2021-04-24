# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Access to read the data from the CSV file (either an interface or a library).
3. Report generator(PDF format) from the battery telematrics data.
4. Notification interface to send the PDF once its ready.
5. Storage capacity of the server to be monitored.

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | This is part of the software being developed
Counting the breaches       | Yes           | This is part of the software being developed
Detecting trends            | Yes           | This is part of the software being developed
Notification utility        | Yes           | This is part of the software being developed

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write "No Data Found" to th PDF when the csv is empty.
4. Write "Access denied" to the PDF when there is no access server.
5. Write "Breach Detected" to the PDF from a csv containing readings greater than the threshold.
6. Write "Date and time" to the PDF when readings continously increased for 30min.
7. PDF report should be generated when a week is completed.
8. Notification should be triggered when the PDF report is generated.
9. Console message "Successfully connected to the sever" when connection to the server containg CSV file.
10. Console message "Connection failed to the server" when connection to the server got failed.


### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality              | Input                             | Output                      | Faked/mocked part
|----------------------------|-----------------------------------|-----------------------------|-----------------------------
| Read input from server     | csv file                          | internal data-structure     | Fake the server store
| Validate input             | csv data                          | valid / invalid             | None - it's a pure function
| Notify report availability | PDF                               | Message sent or failed      | Mock
| Report inaccessible server | Invalid server address/credential | Error Message               | Fake the server
| Find minimum and maximum   | csv data                          | Minimum/Maximum             | None - it's a pure function
| Detect trend               | csv data                          | Date and Time               | None - it's a pure function
| Write to PDF               | Internal data                     | PDF                         | None - it's a pure function
