---
sidebar_position: 3
---

# Get Hybrid Participants

The function is called `oc_get_participants_hybrid`.
This is the function used in the "old" platform.

#### URL
The url to call the function is
```
https://europe-west3-oc-serverless-zoom-functions.cloudfunctions.net/oc_get_participants_hybrid
```

#### Input
Input data MUST contain `meeting_id` field, otherwise it won't work.
It will respond with an error, stating that the meeting id is missing

It can contain `filter` field (no value required).
If is contained, the Limesurvey answers are filtered with the start
and end time of the meeting

#### Header
It MUST contain the authorization bearer and the content-type.

The authorization bearer can be fetched using the gcloud command
`gcloud auth print-identity-token` if you have the correct permissions.

#### Example run

Minimal run
```
curl "https://europe-west3-oc-serverless-zoom-functions.cloudfunctions.net/oc_get_participants_hybrid" \
-H "Authorization: bearer $(gcloud auth print-identity-token)" \
-H "Content-Type:application/json" \
--data '{"meeting_id":"https://zoom/71231512541"}'
```

With filtering
```
curl "https://europe-west3-oc-serverless-zoom-functions.cloudfunctions.net/oc_get_participants_hybrid" \
-H "Authorization: bearer $(gcloud auth print-identity-token)" \
-H "Content-Type:application/json" \
--data '{"meeting_id":"https://zoom/71231512541", "filter":""}'
```

#### Response

The response is a json file which contains zoom report and the list of participants
The json file should contain several keys
```
'all_participants', 'dept', 'duration', 'end_time', 'host_id', 'id', 'participants_count', 'participants_report', 'start_time', 'topic', 'total_minutes', 'tracking_fields', 'type', 'user_email', 'user_name', 'uuid'
```

The actual list of participants is in `all_participants`.
The content of `all_participants` is a list.
Each list item is a python dictionary with the following keys
```
'name', 'email', 'join_time', 'leave_time', 'duration', 'type', 'place'
```
Where
- `name` should be always filled.
- `'email', 'leave_time', 'duration'` only for the zoom participants,
- `join_time` is the join_time of the zoom meeting or the filling time for the survey.
- `type` is `offline` or `online`
- place can be `zoom` or the actual place

##### Check the response
Assuming we saved the response in a resp.json file, we can (in python)
```python
with open("resp.json", "r") as read_file:
    response = json.load(read_file)
    # these are all participants
    hybrid_participants = response['all_participants']
    # each of them is a dict
    for h_part in hybrid_participants:
        ... # h_part is a dict (h_part['name'] for example)
```
