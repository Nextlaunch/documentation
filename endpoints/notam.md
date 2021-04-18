# NOTAM Documentation

## Endpoints
|Path|Summary|
|:---:|:---:|
|[`/`](#root)|Provides a paginated list allowing access to all of the stored NOTAMs in the system|
|[`/upcoming`](#upcoming)|Provides a paginated list for upcoming NOTAMs|
|[`/active`](#active)|Provides a paginated list for active NOTAMs|
|[`/previous`](#previous)|Provides a paginated list for expired and withdrawn NOTAMs|
|[`/:id`](#by-id)|Provides access to individual NOTAMs|

<details>
<summary>### / {#root}
</summary>

<br>
The root path of this endpoint provides access to a paginated list of all NOTAMs currently stored in the system.

#### Parameters

|Name|Example|Description|
|:---:|:---:|:---:|
|limit|limit=20|The number of entries to return (max 100)|
|offset|offset=20|The number of entries to skip before returning data|

#### Sample URL

```
https://nextlaunch.org/api/0.0.1/notams?limit=20&offset=20
```
</details>

<details>
<summary>### /upcoming {#upcoming}
</summary>

<br>
This endpoint provides access to a paginated list of all NOTAMs in the system which meet the following conditions:
- Start time has not passed
- NOTAM is not cancelled or withdrawn

#### Parameters

|Name|Example|Description|
|:---:|:---:|:---:|
|limit|limit=20|The number of entries to return (max 100)|
|offset|offset=20|The number of entries to skip before returning data|

#### Sample URL

```
https://nextlaunch.org/api/0.0.1/notams/upcoming?limit=20&offset=20
```

</details>


<details>
<summary>### /active {#active}
</summary>

<br>
This endpoint provides access to a paginated list of all NOTAMs in the system which meet the following conditions:
- Start time has passed
- End time has not passed
- NOTAM is not cancelled or withdrawn

#### Parameters

|Name|Example|Description|
|:---:|:---:|:---:|
|limit|limit=20|The number of entries to return (max 100)|
|offset|offset=20|The number of entries to skip before returning data|

#### Sample URL

```
https://nextlaunch.org/api/0.0.1/notams/active?limit=20&offset=20
```
</details>


<details>
<summary>### /previous {#previous}
</summary>

<br>
This endpoint provides access to a paginated list of all NOTAMs in the system which meet the following conditions:
- End time has passed OR NOTAM is cancelled or withdrawn

#### Parameters

|Name|Example|Description|
|:---:|:---:|:---:|
|limit|limit=20|The number of entries to return (max 100)|
|offset|offset=20|The number of entries to skip before returning data|

#### Sample URL

```
https://nextlaunch.org/api/0.0.1/notams/previous?limit=20&offset=20
```
</details>


<details>
<summary>### /:id {#by-id}
</summary>

<br>
This endpoint provides access to a single NOTAM

#### Arguments

|Name|Expected Type|Examples|Description|
|:---:|:---:|:---:|:---:|
|id|UUID(v4)/String|`69d06e5a-7ee1-409d-a092-d017e65ff830` or `F1237_21`|The ID of the entry to return|

#### Sample URLs

```
https://nextlaunch.org/api/0.0.1/notams/69d06e5a-7ee1-409d-a092-d017e65ff830
```

```
https://nextlaunch.org/api/0.0.1/notams/F1237_21
```
</details>