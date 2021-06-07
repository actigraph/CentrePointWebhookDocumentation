# Cp2 Daily Statistics Complete Event

Triggered when the processing/ingestion of cp2 daily statistics aggregates has completed for a given day.

**Webhook event name:**

`cp2_daily_statistics_complete`

**Webhook Payload Properties:**

|Name|Type|Description|
|:---|:---|:----------|
|studyId|Number|CentrePoint Study ID|
|subjectId|Number|CentrePoint Subject ID|
|siteId|Number|CentrePoint Site ID|
|dayStatId|Number|Daily Statistics Record ID|
|subjectIdentifier|String|CentrePoint Subject Identifier|
|date|String (ISO8601 Date/Time)|Date of daily statistics record in subject's timezone|
|bouts|Object (see Bouts)|Bout classification in buckets|
|calories|Number|A daily aggregate of calories expended for a subject|
|cutpoints|Object (see Cutpoints)|Classification of a level of activity|
|axisXCounts|Number|A daily aggregate of the X axis counts from the non-partial epochs for subject|
|axisYCounts|Number|A daily aggregate of the Y axis counts from the non-partial epochs for subject|
|axisZCounts|Number|A daily aggregate of the Z axis counts from the non-partial epochs for subject|
|epochs|Number|Total minutes of data for the day for subject|
|mvpa|Number|A daily aggregate including the summation for the Staudenmayer Activity Intensity Cut Point between “Moderate” and “Vigorous”|
|steps|Number|Total steps for day|
|totalMinutes|Number|Total minutes for day|
|wearFilteredBouts|Object (see Bouts)|Bout classification in buckets that represent when subject was wearing device|
|wearFilteredCalories|Number|A daily aggregate of calories expended for a subject that represent when subject was wearing device|
|wearFilteredCutPoints|Object (see Cutpoints)|Classification of a level of activity that represent when subject was wearing device|
|wearFilteredAxisXCounts|Number|A daily aggregate of the X axis counts from the non-partial epochs for subject that represent when subject was wearing device|
|wearFilteredAxisYCounts|Number|A daily aggregate of the Y axis counts from the non-partial epochs for subject that represent when subject was wearing device|
|wearFilteredAxisZCounts|Number|A daily aggregate of the Z axis counts from the non-partial epochs for subject that represent when subject was wearing device|
|wearFilteredMVPA|Number|A daily aggregate including the summation for the Staudenmayer Activity Intensity Cut Point between “Moderate” and “Vigorous” that represent when subject was wearing device|
|wearFilteredSteps|Number|Total steps for day that represent when subject was wearing device|
|wearMinutes|Number|A daily aggregate, in minutes, of the non-partial epochs for subject that represent when subject was wearing device based on wear detection algorithm|
|awakeWearMinutes|Number|A daily aggregate of the non-partial epochs for subject that represent when subject was wearing device and awake|
|awakeWearFilteredAxisXCounts|Number|A daily aggregate of the X axis counts from the non-partial epochs for subject that represent when subject was wearing device and awake|
|awakeWearFilteredAxisYCounts|Number|A daily aggregate of the Y axis counts from the non-partial epochs for subject that represent when subject was wearing device and awake|
|awakeWearFilteredAxisZCounts|Number|A daily aggregate of the Z axis counts from the non-partial epochs for subject that represent when subject was wearing device and awake|
|awakeWearFilteredMVPA|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is between “Moderate” and “Vigorous” representing when subject was wearing the device and awake|
|awakeWearFilteredCutPoints|Object (see Cutpoints)|Classification of a level of activity that represent when subject was wearing device and awake|
|awakeWearFilteredBouts|Object (see Bouts)|Bout classification in buckets that represent when subject was wearing device and awake|
|awakeWearFilteredCalories|Number|A daily aggregate of calories expended for a subject that represent when subject was wearing device and awake|
|awakeWearFilteredSteps|Number|Total steps for day that represent when subject was wearing device and awake|

## Bouts

|Name|Type|Description|
|:---|:---|:----------|
|Name|String|Bout bucket name|
|Count|Number|The number of times a bout occurred during the day|

## Cutpoints

|Name|Type|Description|
|:---|:---|:----------|
|Name|String|Cutpoint bucket name|
|Count|Number|Summation of minutes for the activity level classification|

**Webhook payload example:**

The following are the parameters within the webhook request when upload processing is started

```http
POST <webhook uri goes here>
host: ennr7mfrika8q.x.pipedream.net
content-type: application/json; charset=utf-8
request-context: appId=cid-v1:d39b3fc7-69a6-4aec-bca4-4d53b4b4bb3e
request-id: |bba36cc5d88bb84985ec30e5b934efe5.0cbf24f10a330747.
traceparent: 00-bba36cc5d88bb84985ec30e5b934efe5-0cbf24f10a330747-00
x-ActiGraph-Webhook-id: 27,
x-ActiGraph-Event: cp2_daily_statistics_complete,
x-ActiGraph-Delivery: d97b7b71-4dcd-abc8-3a43-4fba3e5f8b86,
x-Client-Cert-Used: false,
user-Agent: ActiGraph-Hookshot/1.0
{
  "studyId": 34583,
  "subjectId": 17920,
  "siteId": 2937,
  "dayStatId": 1869240,
  "subjectIdentifier": "000103",
  "date": "2013-08-07T00:00:00",
  "bouts": [
    {
      "name": "10 minutes or more",
      "count": 0
    },
    {
      "name": "20 minutes or more",
      "count": 0
    },
    {
      "name": "30 minutes or more",
      "count": 0
    },
    {
      "name": "40 minutes or more",
      "count": 0
    }
  ],
  "calories": 75.980322277385909,
  "cutpoints": [
    {
      "name": "Sedentary",
      "count": 510
    },
    {
      "name": "Light",
      "count": 33
    },
    {
      "name": "Lifestyle",
      "count": 24
    },
    {
      "name": "Moderate",
      "count": 2
    },
    {
      "name": "Vigorous",
      "count": 0
    },
    {
      "name": "Very Vigorous",
      "count": 0
    }
  ],
  "axisXCounts": 49469,
  "axisYCounts": 50215,
  "axisZCounts": 68151,
  "epochs": 569,
  "mvpa": 2,
  "steps": 1296.0,
  "totalMinutes": 569,
  "wearFilteredBouts": [
    {
      "name": "10 minutes or more",
      "count": 0
    },
    {
      "name": "20 minutes or more",
      "count": 0
    },
    {
      "name": "30 minutes or more",
      "count": 0
    },
    {
      "name": "40 minutes or more",
      "count": 0
    }
  ],
  "wearFilteredCalories": 94.965657393572229,
  "wearFilteredCutPoints": [
    {
      "name": "Sedentary",
      "count": 138
    },
    {
      "name": "Light",
      "count": 33
    },
    {
      "name": "Lifestyle",
      "count": 24
    },
    {
      "name": "Moderate",
      "count": 2
    },
    {
      "name": "Vigorous",
      "count": 0
    },
    {
      "name": "Very Vigorous",
      "count": 0
    }
  ],
  "wearFilteredAxisXCounts": 49469,
  "wearFilteredAxisYCounts": 50215,
  "wearFilteredAxisZCounts": 68151,
  "wearFilteredMVPA": 2,
  "wearFilteredSteps": 1296.0,
  "wearMinutes": 197,
  "awakeWearMinutes": 133,
  "awakeWearFilteredAxisXCounts": 37479,
  "awakeWearFilteredAxisYCounts": 39628,
  "awakeWearFilteredAxisZCounts": 52753,
  "awakeWearFilteredMVPA": 2,
  "awakeWearFilteredCutPoints": [
    {
      "name": "Sedentary",
      "count": 91
    },
    {
      "name": "Light",
      "count": 20
    },
    {
      "name": "Lifestyle",
      "count": 20
    },
    {
      "name": "Moderate",
      "count": 2
    },
    {
      "name": "Vigorous",
      "count": 0
    },
    {
      "name": "Very Vigorous",
      "count": 0
    }
  ],
  "awakeWearFilteredBouts": [
    {
      "name": "10 minutes or more",
      "count": 0
    },
    {
      "name": "20 minutes or more",
      "count": 0
    },
    {
      "name": "30 minutes or more",
      "count": 0
    },
    {
      "name": "40 minutes or more",
      "count": 0
    }
  ],
  "awakeWearFilteredCalories": 75.980322277385909,
  "awakeWearFilteredSteps": 1011.0
}
```

## More information

- [Overview](https://github.com/actigraph/WebhookDocumentation)
- [Managing Webhooks](managing_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md)
- [Validating Webhooks](validating_webhooks.md)