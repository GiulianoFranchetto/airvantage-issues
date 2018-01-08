# airvantage-issues
This repository lists the issues found on the airvantage documentation.  
The documentation can be found here: https://doc.airvantage.net/av/reference/cloud/API/

# Authentication
## Overview
> All API access is over HTTPS and accessed from the na.airvantage.net/api/v1 or eu.airvantage.net/api/v1 URL  

- [ ] This sentence is wrong, as all auth endpoints do not contain /v1
  
## Request token
### URL:
/api/oauth/token [POST]
### Parameters:
- [ ] redirect\_uri	is not needed in this request (I'm not even sure it does anything)

# Overall issues
We need to know precisely the format of the JSON response. Some request has different response depending on the state of a system for example (see issue below). Not knowing that some fields could be missing may throw NPE exception in Java for exemple. If we have this information, we can mark the field as ``` @Nullable ``` which will tell the developper to do a runtime check before calling an object field.   

# System
## JSON
- [ ] The full JSON is missing the ```dataUsage ``` object.  
In case of an inactive SIM:
```json
"dataUsage":
  {
    "bytesTotal":null,
    "timestamp":null
  }
```
In case of an active SIM:
```json
 "dataUsage": {
    "bytesTotal": 33792,
    "timestamp": 1513689300000,
    "status": "WITHIN_PLAN",
    "pricePlan": "Bundle ADVANCED Europe 0.5MB",
    "limit": 524288
  }
```
- [ ] The full JSON is missing the ```labels ``` array
```json
 "labels": [
  ]
```

- [ ] The field ``` subscription ``` is duplicated in an array called ```subscriptions```:
```json
  "subscriptions": [
    {
      "identifier": "",
      "state": "INVENTORY",
      "uid": "",
      "mobileNumber": null,
      "networkIdentifier": null,
      "ipAddress": null,
      "technology": "4G",
      "orderId": "",
      "operator": "SIERRA_WIRELESS",
      "requestedIp": null,
      "eid": null,
      "mobileNumber2": null,
      "productRefName": "",
      "appletGeneration": "",
      "confType": "",
      "formFactor": ""
    }
  ]
```
- [ ] The  ```data``` object is missing some fields:
  - ``` "usagesBytesTotal": "" ```
  - ``` "firmwareComponents": null ```
  - ``` "lastTemplateName": null ```
  - ``` "monthBytesTotal": null ``` 
  - ``` "alertState": false ```
  - ``` "alertStateChangeDate": null ```

- [ ] The ```offer``` object is missing the array ```types```:
```json
  "types": [
    "ADVANCED2"
  ]
```
- [ ] The  ```subscription``` object is missing some fields:
  - ``` "orderId": "" ```
  - ``` "mobileNumber2": null ```
  - ``` "productRefName": "" ```

## Find
> Returned systems are shown only with the following attributes uid, name, state, type, lifeCycleState, activityState, creationDate, activationDate, lastStateChangeDate, lastCommDate, commStatus, lastSyncDate, syncStatus To display more or less attributes, the fields parameter has to be set.

- [ ] Wrong

## Activate
- [ ] In the field array, this line is wrong: shall be uid array
> systems.uids	List of system uids to be used to launch the operation	required		uid

