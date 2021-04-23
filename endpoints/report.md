# Report Documentation

## Endpoints

|Path|Summary|
|:---:|:---:|
|[`/`](#root)|Provides a list of all the entities modified within the system in the last 24 hours|


<details>
<summary>### Alert Details
</summary>

<br>
<details open>

<summary>Schema
</summary>

<br>

### Base {#alert-base}

|Field|Type|Description|
|:---:|:---:|:---:|
|id|UUID(v4)/String|The ID of the TFR or NOTAM|
|name|String|The identifier provided by the source|
|type|String|Explains what this entity was produced from<br>One of:<br>`Temporary Flight Restriction`<br>`Notice To Airmen`|
|location|String|The location affected by the TFR (For NOTAMs this is reported as `Unknown`)
|revision|Number|The number of times the entity has been updated|
|added|Timestamp|The time this alert was added to our system|
|start|Timestamp|The time this alert goes into effect|
|end|Timestamp|The time this alert is supposed to expire|
|status.id|Number|A unique numeric value to denote the value of the name field|
|status.name|String|A unique text value to denote the status of the entity|
|altitude|String|The altitude range affected by this alert.|
|report|String|The report text of the alert. Maps to the following:<br>`TFR.text`<br>`NOTAM.rawText`|
|mapLink|String/Null|Link to the map for this alert

### Top level entity {#alert-tle}
The top level of each entity extends the [base](#alert-base) type with one additional field:

|Field|Type|Description|
|:---:|:---:|:---:|
|history|Array<[Base](#alert-base)>|This field is not present on the [base](#alert-base) class because all entities inside of it are already inside of an array containing all historical changes to this entity.|

</details>
<br>
<br>
<details>

<summary>
Sample
</summary>
<br>

```json
{
    "id": "9a7ecf08-ab0a-47ed-96c4-22cd3714733f",
    "name": "1/4940",
    "type": "Temporary Flight Restriction",
    "location": "Cape canaveral, Florida",
    "revision": 1,
    "added": "2021-04-23T00:00:00.000Z",
    "start": "2021-04-28T02:30:00.000Z",
    "end": "2021-04-28T05:58:00.000Z",
    "status": {
        "id": 2,
        "name": "Upcoming"
    },
    "altitude": "From the surface up to and including FLight Level 180",
    "report": "!FDC 1/4940 ZJX FL..AIRSPACE CAPE CANAVERAL, FL..TEMPORARY FLIGHT RESTRICTION. PURSUANT TO 14 CFR SECTION 91.143, SPACE OPERATIONS AREA, AIRCRAFT OPERATIONS ARE PROHIBITED WITHIN AN AREA DEFINED AS 285116N0804219W (OMN141034.4) TO 290730N0803000W (OMN108033.9) THEN CLOCKWISE ON A 30 NM ARC CENTERED ON 283703N0803647W (OMN147048.7) TO 281330N0801600W (OMN145078.4) TO 282501N0803029W (OMN149061.9) TO 282501N0803759W (OMN155058.8) TO 282501N0804144W (OMN157057.4) TO 283121N0804349W (OMN157050.9) TO 283801N0804701W (OMN157043.7) TO 284910N0805044W (OMN154032.2) TO THE POINT OF ORIGIN SFC-FL180 EFFECTIVE 2104280230 UTC UNTIL 2104280558 UTC. 2104280230-2104280558",
    "mapLink": "https://tfr.faa.gov/save_maps/sect_1_4940.gif",
    "history": [
        {
            "id": "f71145ea-e680-4051-b4da-36ca13173708",
            "name": "1/4940",
            "type": "Temporary Flight Restriction",
            "location": "Cape canaveral, Florida",
            "revision": 0,
            "added": "2021-04-22T00:00:00.000Z",
            "start": "2021-04-25T02:30:42.000Z",
            "end": "2021-04-28T05:58:00.000Z",
            "status": {
                "id": 2,
                "name": "Upcoming"
            },
            "altitude": "From the surface up to and including FLight Level 180",
            "report": "!FDC 1/4940 ZJX FL..AIRSPACE CAPE CANAVERAL, FL..TEMPORARY FLIGHT RESTRICTION. PURSUANT TO 14 CFR SECTION 91.143, SPACE OPERATIONS AREA, AIRCRAFT OPERATIONS ARE PROHIBITED WITHIN AN AREA DEFINED AS 285116N0804219W (OMN141034.4) TO 290730N0803000W (OMN108033.9) THEN CLOCKWISE ON A 30 NM ARC CENTERED ON 283703N0803647W (OMN147048.7) TO 281330N0801600W (OMN145078.4) TO 282501N0803029W (OMN149061.9) TO 282501N0803759W (OMN155058.8) TO 282501N0804144W (OMN157057.4) TO 283121N0804349W (OMN157050.9) TO 283801N0804701W (OMN157043.7) TO 284910N0805044W (OMN154032.2) TO THE POINT OF ORIGIN SFC-FL180 EFFECTIVE 2104280230 UTC UNTIL 2104280558 UTC. 2104280230-2104280558",
            "mapLink": "https://tfr.faa.gov/save_maps/sect_1_4940.gif"
        }
    ]
}
```

</details>
</details>

<br>

### / {#root}

<br>
Provides a list of all the entities modified within the system in the last 24 hours

#### Parameters

None

#### Sample URL

```
https://nextlaunch.org/api/0.0.1/report
```

### Response format
The response contains two fields, `tfr` and `notam` each of which has the following:
- `upcoming` Array<[Top Level Entity](#alert-base)>
- `active` Array<[Top Level Entity](#alert-base)>
- `expired` Array<[Top Level Entity](#alert-base)>
- `withdrawn` Array<[Top Level Entity](#alert-base)>

This schema can be expressed as below:

```json
{
    "tfr": {
        "upcoming": [...Top Level Entity],
        "active": [...Top Level Entity],
        "expired": [...Top Level Entity],
        "withdrawn": [...Top Level Entity]
    },
    "notam": {
        "upcoming": [...Top Level Entity],
        "active": [...Top Level Entity],
        "expired": [...Top Level Entity],
        "withdrawn": [...Top Level Entity]
    }
}
```