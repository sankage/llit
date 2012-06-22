LLIT (Limited List Importing Tool)
==================================

A tool to handle cases when new respondent lists need to be vetted against previous lists to remove recent invitees.

## PURPOSE
To export and/or upload a respondent list into a survey platform that has had recent respondents removed from the list.

## INTERFACE

### LLIT::RespondentList
Contains all the needed parts of a respondent list. A lists Respondent objects will be stored as an Array under the `@respondents` attribute.

- `#parse` (path_name) takes in the pathname to the csv file and generates Respondent objects
- `#check` checks each Respondent for recentness
- `#upload` runs Respondent#upload for each member of the list
- `#export` returns a csv of the list

### LLIT::Respondent
Contains all the needed parts of a survey respondent (1 row of the csv). Ideally instance attributes would match the header row of the csv, but to prevent any name collisions with methods, they are stored as a hash under the attribute `@fields`.

- `#check` checks this respondent against the survey platform
- `#upload` uploads the respondent to the survey platform

### LLIT::SurveyAPI
Contains all the needed parts to establish an API connection with the survey platform.

- `#add_respondent` (Respondent) adds a respondent to the survey platform, returns True on success
- `#recent_respondent?` (Respondent, Date) checks to see if the Respondent has taken the survey since Date, returns True if they have