---
sidebar_position: 2
---

# Attendances

The attendances registration function should work automatically in the background. It lies in the google cloud platform and is a serverless function triggered from a time trigger each X hours or once per day.

### Workflow

The workflow is the following:

1. the function queries hasura for the current program (semester).
2. with the current program, it fetches all the past session (from program start to today) and the attendance table
3. it fetches all the offline response via limsurvey (this could be also done later, but is to be done only once, all responses are in the same survey)
4. it calculates which sessions are still not checked (there are no results in the attendance table)
5. for each unchecked session, it asks zoom for the list of online participants, filter it and merges it with the offline one (only the one related to the course); it also asks hasura for the registered participants of the related course.
6. it matches the participants (merged list online + offline against the registered one from the course).
7. it writes to the attendance table

### Environmental Variables

It requires a configuration files (`.env`) with the following variables:

```
api_key= #zoom
api_secret= #zoom
hasura_admin_secret=
hasura_url=
lms_url= #limesurvey url
lms_user=
lms_password=
lms_sID= #surveyID
```

### Code

Not deployed yet - soon to be updated
