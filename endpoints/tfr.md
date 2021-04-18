# TFR Documentation

## Endpoints
|Path|Summary|
|:---:|:---:|
|[`/`](#root)|Provides a paginated list allowing access to all of the stored TFRs in the system|
|[`/upcoming`](#upcoming)|Provides a paginated list for upcoming TFRs|
|[`/active`](#active)|Provides a paginated list for active TFRs|
|[`/previous`](#previous)|Provides a paginated list for expired and withdrawn TFRs|
|[`/:id`](#by-id)|Provides access to individual TFRs|

<details>
<summary>### / {#root}
</summary>

<br>
The root path of this endpoint provides access to a paginated list of all TFRs currently stored in the system.

#### Parameters

|Name|Example|Description|
|:---:|:---:|:---:|
|limit|limit=20|The number of entries to return (max 100)|
|offset|offset=20|The number of entries to skip before returning data|

#### Sample URL
```http request
https://nextlaunch.org/api/0.0.1/tfr?limit=20&offset=20
```
</details>

<details>
<summary>### /upcoming {#upcoming}
</summary>

<br>
This endpoint provides access to a paginated list of all TFRs in the system which meet the following conditions:
- Start time has not passed
- TFR is not cancelled or withdrawn

#### Parameters

|Name|Example|Description|
|:---:|:---:|:---:|
|limit|limit=20|The number of entries to return (max 100)|
|offset|offset=20|The number of entries to skip before returning data|

#### Sample URL
```http request
https://nextlaunch.org/api/0.0.1/tfr/upcoming?limit=20&offset=20
```
</details>


<details>
<summary>### /active {#active}
</summary>

<br>
This endpoint provides access to a paginated list of all TFRs in the system which meet the following conditions:
- Start time has passed
- End time has not passed
- TFR is not cancelled or withdrawn

#### Parameters

|Name|Example|Description|
|:---:|:---:|:---:|
|limit|limit=20|The number of entries to return (max 100)|
|offset|offset=20|The number of entries to skip before returning data|

#### Sample URL
```http request
https://nextlaunch.org/api/0.0.1/tfr/active?limit=20&offset=20
```
</details>


<details>
<summary>### /previous {#previous}
</summary>

<br>
This endpoint provides access to a paginated list of all TFRs in the system which meet the following conditions:
- End time has passed OR TFR is cancelled or withdrawn

#### Parameters

|Name|Example|Description|
|:---:|:---:|:---:|
|limit|limit=20|The number of entries to return (max 100)|
|offset|offset=20|The number of entries to skip before returning data|

#### Sample URL
```http request
https://nextlaunch.org/api/0.0.1/tfr/previous?limit=20&offset=20
```
</details>


<details>
<summary>### /:id {#by-id}
</summary>

<br>
This endpoint provides access to a single TFR

#### Arguments

|Name|Expected Type|Examples|Description|
|:---:|:---:|:---:|:---:|
|id|UUID(v4)/String|`797d0a62-3aab-460e-9881-f18f2bd1bc97` or `1_4530`|The ID of the entry to return|

#### Sample URLs
```http request
https://nextlaunch.org/api/0.0.1/tfr/797d0a62-3aab-460e-9881-f18f2bd1bc97
```
```http request
https://nextlaunch.org/api/0.0.1/tfr/1_4530
```
</details>