# Daily Statistics Complete Event

Triggered when the processing/ingestion of daily statistics aggregates has completed for a given day.

**Webhook event name:**

`daily_statistics_complete`

**Webhook Payload Parameters:**

|Name|Type|Description|
|:---|:---|:----------|
|id|Number|Daily Statistics Record ID|
|studyId|Number|CentrePoint Study ID|
|siteId|Number|CentrePoint Site ID|
|subjectId|Number|CentrePoint Subject ID|
|date|String (ISO8601 Date/Time)|Date of daily statistics record in subject's timezone|
|activityMonitorSerials|Array of String|Activity monitor serial number(s) which contributed data to the daily statistic record|
|epochAggregation|Object|Contains daily summary of epoch data|
|freedsonAggregations|Object|Contains daily summary of Freedson cutpoints|
|mavmAggregation|Object|Contains daily summary of MAVMv1 steps|
|crouterAggregations|Object|Contains daily summary of Crouter-Child cutpoints|
|staudenmayerAggregations|Object|Contains daily summary of Staudenmayer cutpoints|
|uwfAggregations|Object|Contains daily summary of UWF steps|

## Epoch Aggregation

|Name|Type|Description|
|:---|:---|:----------|
|wearMinutes|Number|A daily aggregate, in minutes, of the non-partial epochs for subject that represent when subject was wearing device based on wear detection algorithm|
|nonWearMinutes|Number|A daily aggregate, in minutes, of the non-partial epochs for subject that represent when subject was not wearing device based on wear detection algorithm|
|sleepMinutes|Number|A daily aggregate of the non-partial epochs for subject that represent when the subject was asleep based on sleep detection algorithm|
|awakeMinutes|Number|A daily aggregate of the non-partial epochs for subject that represent when the subject was awake|
|wearAwakeMinute|Number|A daily aggregate of the non-partial epochs for subject that represent when subject was wearing device and awake|
|wearSleepMinutes|Number|A daily aggregate of the non-partial epochs for subject that represent when subject was wearing device and asleep|
|totalNonFilteredMinutes|Number|A daily aggregate of the non-partial epochs for given subject not filtered for wear or sleep|
|totalNonFilteredAxisXCounts|Number|A daily aggregate of the X axis counts from the non-partial epochs for subject|
|totalNonFilteredAxisYCounts|Number|A daily aggregate of the Y axis counts from the non-partial epochs for subject|
|totalNonFilteredAxisZCounts|Number|A daily aggregate of the Z axis counts from the non-partial epochs for subject|
|wearFilteredAxisXCounts|Number|A daily aggregate of the X axis counts from the non-partial epochs for subject that represent when subject was wearing device|
|wearFilteredAxisYCounts|Number|A daily aggregate of the Y axis counts from the non-partial epochs for subject that represent when subject was wearing device|
|wearFilteredAxisZCounts|Number|A daily aggregate of the Z axis counts from the non-partial epochs for subject that represent when subject was wearing device|
|wearAwakeFilteredAxisXCounts|Number|A daily aggregate of the X axis counts from the non-partial epochs for subject that represent when subject was wearing device and awake|
|wearAwakeFilteredAxisYCounts|Number|A daily aggregate of the Y axis counts from the non-partial epochs for subject that represent when subject was wearing device and awake|
|wearAwakeFilteredAxisZCounts|Number|A daily aggregate of the Z axis counts from the non-partial epochs for subject that represent when subject was wearing device and awake|
|wearSleepFilteredAxisXCounts|Number|A daily aggregate of the X axis counts from the non-partial epochs for subject that represent when subject was wearing device and asleep|
|wearSleepFilteredAxisYCounts|Number|A daily aggregate of the Y axis counts from the non-partial epochs for subject that represent when subject was wearing device and asleep|
|wearSleepFilteredAxisZCounts|Number|A daily aggregate of the Z axis counts from the non-partial epochs for subject that represent when subject was wearing device and asleep|
|totalNonFilteredVectorMagnitude|Number|A daily aggregate of the Vector Magnitude values (of x, y, and x axis counts) from the non-partial epochs for subject|
|wearFilteredVectorMagnitude|Number|A daily aggregate of the Vector Magnitude values (of x, y, and x axis counts) from the non-partial epochs for subject which represent when subject was wearing the device|
|wearAwakeFilteredVectorMagnitude|Number|A daily aggregate of the Vector Magnitude values (of x, y, and x axis counts) from the non-partial epochs for subject which represent when subject was wearing the device and awake|
|wearSleepFilteredVectorMagnitude|Number|A  daily aggregate of the Vector Magnitude values (of x, y, and x axis counts) from the non-partial epochs for subject which represent when subject was wearing the device and awake|
|firstEpochDateTimeUtc|String (ISO8601 Date/Time)|Date Time in UTC timezone of first epoch recorded foir this day|
|lastEpochDateTimeUtc|String (ISO8601 Date/Time)|Date Time in UTC timezone of first epoch recorded foir this day|
|firstEpochDateTimeLocal|String (ISO8601 Date/Time)|Date Time in subject's timezone of first epoch recorded for this day|
|lastEpochDateTimeLocal|String (ISO8601 Date/Time)|Date Time in subject's timezone of first epoch recorded for this day|

The following sections may be contained in the daily statistics webhook payload based on your study's configuration:

## Freedson Adult (VA) Cut Point Aggregations

|Name|Type|Description|
|:---|:---|:----------|
|nonFilteredVASedentary|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Sedentary”|
|nonFilteredVALight|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Light”|
|nonFilteredVAModerate|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Moderate”|
|nonFilteredVAVigorous|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Vigorous”|
|nonFilteredVAVeryVigorous|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Very Vigorous”|
|wearFilteredVASedentary|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Sedentary” where the subject was wearing the device|
|wearFilteredVALight|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Light” where the subject was wearing the device|
|wearFilteredVAModerate|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Moderate” where the subject was wearing the device|
|wearFilteredVAVigorous|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Vigorous” where the subject was wearing the device|
|wearFilteredVAVeryVigorous|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Very Vigorous” where the subject was wearing the device|
|wearAwakeFilteredVASedentary|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Sedentary” where the subject was wearing the device and awake|
|wearAwakeFilteredVALight|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Light” where the subject was wearing the device and awake|
|wearAwakeFilteredVAModerate|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Moderate” where the subject was wearing the device and awake|
|wearAwakeFilteredVAVigorous|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Vigorous” where the subject was wearing the device and awake|
|wearAwakeFilteredVAVeryVigorous|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Very Vigorous” where the subject was wearing the device and awake|
|wearSleepFilteredVASedentary|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Sedentary” where the subject was wearing the device and asleep|
|wearSleepFilteredVALight|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Light” where the subject was wearing the device and asleep|
|wearSleepFilteredVAModerate|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Moderate” where the subject was wearing the device and asleep|
|wearSleepFilteredVAVigorous|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Vigorous” where the subject was wearing the device and asleep|
|wearSleepFilteredVAVeryVigorous|Number|A daily aggregate where the Freedson Adult Cut Points VA Activity Intensity is “Very Vigorous” where the subject was wearing the device and asleep|

## MAVMv1 Steps Aggregation

|Name|Type|Description|
|:---|:---|:----------|
|nonFilteredSteps|Number|Total steps for day|
|wearFilteredSteps|Number|Total steps where activity monitor was considered worn|
|wearAwakeFilteredSteps|Number|Total steps where activity monitor was worn and subject was considered awake|
|wearSleepFilteredSteps|Number|Total steps where activity monitor was worn and subject was considered asleep|

## Crouter-Child Cutpoint Aggregations

|Name|Type|Description|
|:---|:---|:----------|
|nonFilteredVMSedentary|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Sedentary”|
|nonFilteredVMLight|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Light”|
|nonFilteredVMModerate|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Moderate”|
|nonFilteredVMVigorous|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Vigorous”|
|nonFilteredVMMVPA|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point between “Moderate” and “Vigorous”|
|wearFilteredVMSedentary|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Sedentary” which represent where the subject was wearing the device|
|wearFilteredVMLight|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Light” which represent where the subject was wearing the device|
|wearFilteredVMModerate|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Moderate” which represent where the subject was wearing the device|
|wearFilteredVMVigorous|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Vigorous” which represent where the subject was wearing the device|
|wearFilteredVMMVPA|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is between “Moderate” and “Vigorous” which represent where the subject was wearing the device|
|wearAwakeFilteredVMSedentary|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Sedentary” which represent where the subject was wearing the device and awake|
|wearAwakeFilteredVMLight|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Light” which represent where the subject was wearing the device and awake|
|wearAwakeFilteredVMModerate|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Moderate” which represent where the subject was wearing the device and awake|
|wearAwakeFilteredVMVigorous|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Vigorous” which represent where the subject was wearing the device and awake|
|wearAwakeFilteredVMMVPA|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is between “Moderate” and “Vigorous” which represent where the subject was wearing the device and awake|
|wearSleepFilteredVMSedentary|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Sedentary” which represent where the subject was wearing the device and asleep|
|wearSleepFilteredVMLight|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Light” which represent where the subject was wearing the device and asleep|
|wearSleepFilteredVMModerate|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Moderate” which represent where the subject was wearing the device and asleep|
|wearSleepFilteredVMVigorous|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is “Vigorous” which represent where the subject was wearing the device and asleep|
|wearSleepFilteredVMMVPA|Number|A daily aggregate where the Crouter VM Activity Intensity Cut Point is between “Moderate” and “Vigorous” which represent where the subject was wearing the device and asleep|
|nonFilteredVASedentary|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Sedentary”|
|nonFilteredVALight|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Light”|
|nonFilteredVAModerate|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Moderate”|
|nonFilteredVAVigorous|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Vigorous”|
|nonFilteredVAMVPA|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point between “Moderate” and “Vigorous”|
|wearFilteredVASedentary|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Sedentary” which represent where the subject was wearing the device|
|wearFilteredVALight|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Light” which represent where the subject was wearing the device|
|wearFilteredVAModerate|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Moderate” which represent where the subject was wearing the device|
|wearFilteredVAVigorous|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Vigorous” which represent where the subject was wearing the device|
|wearFilteredVAMVPA|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is between “Moderate” and “Vigorous” which represent where the subject was wearing the device|
|wearAwakeFilteredVASedentary|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Sedentary” which represent where the subject was wearing the device and awake|
|wearAwakeFilteredVALight|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Light” which represent where the subject was wearing the device and awake|
|wearAwakeFilteredVAModerate|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Moderate” which represent where the subject was wearing the device and awake|
|wearAwakeFilteredVAVigorous|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Vigorous” which represent where the subject was wearing the device and awake|
|wearAwakeFilteredVAMVPA|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is between “Moderate” and “Vigorous” which represent where the subject was wearing the device and awake|
|wearSleepFilteredVASedentary|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Sedentary” which represent where the subject was wearing the device and asleep|
|wearSleepFilteredVALight|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Light” which represent where the subject was wearing the device and asleep|
|wearSleepFilteredVAModerate|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Moderate” which represent where the subject was wearing the device and asleep|
|wearSleepFilteredVAVigorous|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is “Vigorous” which represent where the subject was wearing the device and asleep|
|wearSleepFilteredVAMVPA|Number|A daily aggregate where the Crouter VA Activity Intensity Cut Point is between “Moderate” and “Vigorous” which represent where the subject was wearing the device and asleep|

## Staudenmayer Cutpoint Aggregations

|Name|Type|Description|
|:---|:---|:----------|
|nonFilteredLight|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is considered “Light”|
|nonFilteredModerate|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is considered “Moderate”|
|nonFilteredVigorous|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is considered “Vigorous”|
|nonFilteredMVPA|Number|A daily aggregate including the summation for the Staudenmayer Activity Intensity Cut Point between “Moderate” and “Vigorous”|
|nonFilteredSedentary|Number|A daily aggregate where the Staudenmayer Sedentary Intensity Cut Point is “Sedentary”|
|nonFilteredNonSedentary|Number|A daily aggregate where the Staudenmayer Sedentary Intensity Cut Point is “Non-Sedentary”|
|nonFilteredLocomotion|Number|A daily aggregate where the Staudenmayer Locomotion Intensity Cut Point is “Locomotion”|
|nonFilteredNonLocomotion|Number|A daily aggregate where the Staudenmayer Locomotion Intensity Cut Point is “Non-Locomotion”|
|WearFilteredLight|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Light” representing when the subject was wearing the device|
|wearFilteredModerate|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Moderate” representing when the subject was wearing the device|
|wearFilteredVigorous|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Vigorous” representing when the subject was wearing the device|
|wearFilteredMVPA|Number|A daily aggregate where the summation for the Staudenmayer Activity Intensity Cut Point between “Moderate” and “Vigorous” representing when the subject was wearing the device|
|wearFilteredSedentary|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Sedentary” representing when the subject was wearing the device|
|wearFilteredNonSedentary|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Non-Sedentary” representing when the subject was wearing the device|
|wearFilteredLocomotion|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Locomotion” representing when the subject was wearing the device|
|wearFilteredNonLocomotion|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Non-Locomotion” representing when the subject was wearing the device|
|wearAwakeFilteredLight|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Light” representing when subject was wearing the device and awake|
|wearAwakeFilteredModerate|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Moderate” representing when subject was wearing the device and awake|
|wearAwakeFilteredVigorous|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Vigorous” representing when subject was wearing the device and awake|
|wearAwakeFilteredMVPA|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is between “Moderate” and “Vigorous” representing when subject was wearing the device and awake|
|wearAwakeFilteredSedentary|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Sedentary” representing when subject was wearing the device and awake|
|wearAwakeFilteredNonSedentary|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Non-Sedentary” representing when subject was wearing the device and awake|
|wearAwakeFilteredLocomotion|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Locomotion” representing when subject was wearing the device and awake|
|wearAwakeFilteredNonLocomotion|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Non-Locomotion” representing when subject was wearing the device and awake|
|wearSleepFilteredLight|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Light” representing when subject was wearing the device and asleep|
|wearSleepFilteredModerate|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Moderate” representing when subject was wearing the device and asleep|
|wearSleepFilteredVigorous|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Vigorous” representing when subject was wearing the device and asleep|
|wearSleepFilteredMVPA|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is between “Moderate” and “Vigorous” representing when subject was wearing the device and asleep|
|wearSleepFilteredSedentary|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Sedentary” representing when subject was wearing the device and asleep|
|wearSleepFilteredNonSedentary|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Non-Sedentary” representing when subject was wearing the device and asleep|
|wearSleepFilteredLocomotion|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Locomotion” representing when subject was wearing the device and asleep|
|wearSleepFilteredNonLocomotion|Number|A daily aggregate where the Staudenmayer Activity Intensity Cut Point is “Non-Locomotion” representing when subject was wearing the device and asleep|

## University of West Florida Steps Aggregations

|Name|Type|Description|
|:---|:---|:----------|
|nonFilteredSteps|Number|Total steps for day|
|wearFilteredSteps|Number|Total steps where activity monitor was considered worn|
|wearAwakeFilteredSteps|Number|Total steps where activity monitor was worn and subject was considered awake|
|wearSleepFilteredSteps|Number|Total steps where activity monitor was worn and subject was considered asleep|

## Hildebrand MET/Calorie Aggregation

|Name|Type|Description|
|:---|:---|:----------|
|**nonFilteredMets**|Number|Total METS for the day|
|**wearMets**|Number|Total METS where activity monitor was considered worn|
|**wearAwakeMets**|Number|Total METS where activity monitor was worn and subject was considered awake|
|**nonFilteredMetsAverage**|Number|Average METS for the day|
|**wearMetsAverage**|Number|Average METS where activity monitor was considered worn|
|**wearAwakeMetsAverage**|Number|Average METS where activity monitor was worn and subject was considered awake|
|**nonFilteredCalories**|Number|Total Calories for the day|
|**wearCalories**|Number|Total Calories where activity monitor was considered worn|
|**wearAwakeCalories**|Number|Total Calories where activity monitor was worn and subject was considered awake|

**Webhook payload example:**

The following are the parameters within the webhook request when upload processing is started

```http
POST <webhook uri goes here>
host: ennr7mfrika8q.x.pipedream.net
content-type: application/json; charset=utf-8
request-context: appId=cid-v1:d39b3fc7-69a6-4aec-bca4-4d53b4b4bb3e
request-id: |bba36cc5d88bb84985ec30e5b934efe5.0cbf24f10a330747.
traceparent: 00-bba36cc5d88bb84985ec30e5b934efe5-0cbf24f10a330747-00
x-ActiGraph-Webhook-id: 26,
x-ActiGraph-Event: daily_statistics_complete,
x-ActiGraph-Delivery: d97b7b71-4dcd-abc8-3a43-4fba3e5f8b86,
x-Client-Cert-Used: false,
user-Agent: ActiGraph-Hookshot/1.0
{
  "subjectIdentifier": "0123TEST",
  "id": 186,
  "studyId": 234,
  "subjectId": 17887,
  "date": "2017-11-01T05:00:00+00:00",
  "siteId": 2922,
  "activityMonitorSerials": [
    "TAS1Z12345678"
  ],
  "epochAggregation": {
    "wearMinutes": 75.0,
    "nonWearMinutes": 5.0,
    "sleepMinutes": 3.0,
    "awakeMinutes": 77.0,
    "wearAwakeMinutes": 75.0,
    "wearSleepMinutes": 0.0,
    "totalNonFilteredMinutes": 80.0,
    "totalNonFilteredAxisXCounts": 125694,
    "totalNonFilteredAxisYCounts": 102810,
    "totalNonFilteredAxisZCounts": 60718,
    "wearFilteredAxisXCounts": 125640,
    "wearFilteredAxisYCounts": 102810,
    "wearFilteredAxisZCounts": 60718,
    "wearAwakeFilteredAxisXCounts": 125640,
    "wearAwakeFilteredAxisYCounts": 102810,
    "wearAwakeFilteredAxisZCounts": 60718,
    "wearSleepFilteredAxisXCounts": 0,
    "wearSleepFilteredAxisYCounts": 0,
    "wearSleepFilteredAxisZCounts": 0,
    "totalNonFilteredVectorMagnitude": 173365.37503204035,
    "wearFilteredVectorMagnitude": 173326.22774410108,
    "wearAwakeFilteredVectorMagnitude": 173326.22774410108,
    "wearSleepFilteredVectorMagnitude": 0.0,
    "firstEpochDateTimeUtc": "2017-11-01T11:45:00+00:00",
    "lastEpochDateTimeUtc": "2017-11-01T13:04:00+00:00",
    "firstEpochDateTimeLocal": "2017-11-01T11:45:00+00:00",
    "lastEpochDateTimeLocal": "2017-11-01T13:04:00+00:00"
  },
  "freedsonAggregations": [
    {
      "nonFilteredVASedentary": 3180,
      "nonFilteredVALight": 780,
      "nonFilteredVAModerate": 840,
      "nonFilteredVAVigorous": 0,
      "nonFilteredVAVeryVigorous": 0,
      "wearFilteredVASedentary": 2880,
      "wearFilteredVALight": 780,
      "wearFilteredVAModerate": 840,
      "wearFilteredVAVigorous": 0,
      "wearFilteredVAVeryVigorous": 0,
      "wearAwakeFilteredVASedentary": 2880,
      "wearAwakeFilteredVALight": 780,
      "wearAwakeFilteredVAModerate": 840,
      "wearAwakeFilteredVAVigorous": 0,
      "wearAwakeFilteredVAVeryVigorous": 0,
      "wearSleepFilteredVASedentary": 0,
      "wearSleepFilteredVALight": 0,
      "wearSleepFilteredVAModerate": 0,
      "wearSleepFilteredVAVigorous": 0,
      "wearSleepFilteredVAVeryVigorous": 0
    }
  ],
  "staudenmayerAggregations": [
    {
      "nonFilteredLight": 2190,
      "nonFilteredModerate": 1680,
      "nonFilteredVigorous": 930,
      "nonFilteredMVPA": 2610,
      "nonFilteredSedentary": 3120,
      "nonFilteredNonSedentary": 1680,
      "nonFilteredLocomotion": 1860,
      "nonFilteredNonLocomotion": 2940,
      "wearFilteredLight": 2190,
      "wearFilteredModerate": 1380,
      "wearFilteredVigorous": 930,
      "wearFilteredMVPA": 2310,
      "wearFilteredSedentary": 2820,
      "wearFilteredNonSedentary": 1680,
      "wearFilteredLocomotion": 1860,
      "wearFilteredNonLocomotion": 2640,
      "wearAwakeFilteredLight": 2190,
      "wearAwakeFilteredModerate": 1380,
      "wearAwakeFilteredVigorous": 930,
      "wearAwakeFilteredMVPA": 2310,
      "wearAwakeFilteredSedentary": 2820,
      "wearAwakeFilteredNonSedentary": 1680,
      "wearAwakeFilteredLocomotion": 1860,
      "wearAwakeFilteredNonLocomotion": 2640,
      "wearSleepFilteredLight": 0,
      "wearSleepFilteredModerate": 0,
      "wearSleepFilteredVigorous": 0,
      "wearSleepFilteredMVPA": 0,
      "wearSleepFilteredSedentary": 0,
      "wearSleepFilteredNonSedentary": 0,
      "wearSleepFilteredLocomotion": 0,
      "wearSleepFilteredNonLocomotion": 0
    }
  ],
  "mavmAggregation": {
    "nonFilteredSteps": 865,
    "wearFilteredSteps": 865,
    "wearAwakeFilteredSteps": 865,
    "wearSleepFilteredSteps": 0
  },
  "firstEpochDateTimeUtc": "2017-11-01T11:45:00+00:00",
  "lastEpochDateTimeUtc": "2017-11-01T13:04:00+00:00",
  "firstEpochDateTimeLocal": "2017-11-01T11:45:00+00:00",
  "lastEpochDateTimeLocal": "2017-11-01T13:04:00+00:00"
}
```

## More information

- [Overview](https://github.com/actigraph/WebhookDocumentation)
- [Managing Webhooks](managing_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md)
- [Validating Webhooks](validating_webhooks.md)
