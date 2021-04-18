# Nextlaunch Documentation

Welcome to the Nextlaunch documentation. The pages here will guide you through the basics of using our API for your own
projects.

### Before you start

Nextlaunch is a passion project. As such this documentation may stray from the actual behaviour of the API.

Want to try the API out without writing code?

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/a79e7d16088a2d207213)

### Basic Structures

<details>
<summary>
Temporary Flight Restriction (TFR)
</summary>
<br>
<details open>

<summary>
Schema
</summary>

<br>

### Temporary Flight Restriction

|Field|Type|Description|
|:---:|:---:|:---:|
|id|UUID(v4)/String|The ID of the TFR|
|name|String|The identifier provided by the source|
|location|String|The location of affected by the TFR|
|revision|Number|The number of times this TFR has been revised|
|added|Timestamp|The time this TFR revision was added to the database (UTC/Zulu)|
|start|Timestamp|The time this TFR is scheduled to begin (UTC/Zulu)|
|end|Timestamp|The time this TFR is scheduled to end (UTC/Zulu)
|last Detected|Timestamp|The last time this TFR was detected by the system (UTC/Zulu)|
|status|[Status](#tfr-status)|Status information about the TFR
|description|String|A brief description of the TFR|
|text|String|The raw text of the TFR|
|altitudesAffected|[Altitudes](#tfr-altitudes)|Altitude information for the TFR
|links.map|String|A URL to an image of the areas this TFR affects (Provided by the FAA)|
|links.source|String|A URL to this TFR's source page|

### Status {#tfr-status}

|Field|Type|Description|
|:---:|:---:|:---:|
|withdrawal.withdrawn|Boolean|If the TFR has been withdrawn|
|withdrawal.time|Timestamp/Null|The time the TFR was withdrawn (For a more reliable source, use `TFR.lastDetected`|
|expired|Boolean|If the TFR has expired|
|effective|Boolean|If the TFR is considered "in effect" (current time is between start and end, and the TFR has not been withdrawn)|

### Altitudes {#tfr-altitudes}

|Field|Type|Description|
|:---:|:---:|:---:|
|upper.height|Number|The value of the upper limit|
|upper.unit|String|The units that `upper.height` is measured in|
|upper.inclusive|Boolean|Whether the value of `upper.height` is inclusive, or not|
|upper.trusted|Boolean|Whether or not Nextlaunch can trust the data provided in this upper limit|
|lower.height|Number|The value of the lower limit|
|lower.unit|String|The units that `lower.height` is measured in|
|lower.inclusive|Boolean|Whether the value of `lower.height` is inclusive, or not|
|lower.trusted|Boolean|Whether or not Nextlaunch can trust the data provided in this lower limit|
|Message|String|This altitude pairing expressed in a human readable format|

</details>

<details>
<summary>
Sample
</summary>
<br>

```json
{
    "id": "797d0a62-3aab-460e-9881-f18f2bd1bc97",
    "name": "1/4530",
    "location": "Cape canaveral, Florida",
    "revision": 0,
    "added": "2021-04-04T00:00:00.000Z",
    "start": "2021-04-07T15:00:00.000Z",
    "end": "2021-04-07T17:24:00.000Z",
    "lastDetected": "2021-04-07T17:28:06.744Z",
    "status": {
        "withdrawal": {
            "withdrawn": true,
            "time": "2021-04-07T17:28:06.744Z"
        },
        "expired": true,
        "effective": false
    },
    "description": "CAPE CANAVERAL, FL, Wednesday, April 07, 2021 UTC",
    "text": "!FDC 1/4530 ZJX FL..AIRSPACE CAPE CANAVERAL, FL..TEMPORARY FLIGHT RESTRICTION. PURSUANT TO 14 CFR SECTION 91.143, SPACE OPERATIONS AREA, AIRCRAFT OPERATIONS ARE PROHIBITED WITHIN AN AREA DEFINED AS 285116N0804219W (OMN141034.4) TO 290730N0803000W (OMN108033.9) THEN CLOCKWISE ON A 30 NM ARC CENTERED ON 283703N0803647W (OMN147048.7) TO 281330N0801600W (OMN145078.4) TO 282501N0803029W (OMN149061.9) TO 282501N0803759W (OMN155058.8) TO 282501N0804144W (OMN157057.4) TO 283121N0804349W (OMN157050.9) TO 283801N0804701W (OMN157043.7) TO 284910N0805044W (OMN154032.2) TO THE POINT OF ORIGIN SFC-FL180 EFFECTIVE 2104071500 UTC UNTIL 2104071724 UTC. 2104071500-2104071724",
    "altitudesAffected": {
        "upper": {
            "height": 180,
            "unit": "FL",
            "inclusive": true,
            "trusted": true
        },
        "lower": {
            "height": 0,
            "unit": "FL",
            "inclusive": true,
            "trusted": true
        },
        "message": "From the surface up to and including FLight Level 180"
    },
    "links": {
        "map": "https://tfr.faa.gov/save_maps/sect_1_4530.gif",
        "source": "https://tfr.faa.gov/save_pages/detail_1_4530.html"
    }
}

```

</details>
</details>