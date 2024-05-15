# Metar & Taf API

[Home](../README.md)・Metar & Taf API


## Endpoints

### Base URL

`https://weather-data-dev2.atmosoar.io`

#### Get METAR or TAF data for a specified airport

<details>
<summary>
    <code>GET</code> <code><b>/api/{type}/station/{icao}</b></code>
</summary>

##### Parameters:

| name      | type   | required | description                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------|
|  type  | string | yes      | Type of data to retrieve (metar or taf)                                   |
|  icao  | string | yes      | ICAO code of the airport                                  |



##### Responses:

| http code     | content-type                      | response               |
|---------------|-----------------------------------|------------------------|
| `200`         | `application/json`                |                        |


##### Example:

```javascript
const baseUrl = "https://weather-data-dev2.atmosoar.io";

async function loadWeatherData(type, icao) {

    const url = baseUrl + '/api/' + type + '/station/' icao;

    const response = await fetch(url);
    const responseData = await response.json();
    console.log(responseData[type]);
}
```
</details>

#### Get METAR or TAF data for a specified area

<details>
<summary>
    <code>GET</code> <code><b>/api/{type}/area</b></code>
</summary>

##### Parameters:

| name      | type   | required | description                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------|
| type      | string | yes      | Type of data to retrieve (metar or taf)                                    |
| north     | number | yes      | Northern latitude of the area in decimal degrees                           |
| south     | number | yes      | Southern latitude of the area in decimal degrees                           |
| east      | number | yes      | Eastern longitude of the area in decimal degrees                           |
| west      | number | yes      | Western longitude of the area in decimal degrees                           |


##### Responses:

| http code     | content-type                      | response               |
|---------------|-----------------------------------|------------------------|
| `200`         | `application/json`                |                        |


##### Example:

```javascript
const baseUrl = "https://weather-data-dev2.atmosoar.io"; 

async function loadAreaWeatherData(type, area) {
    const url = baseUrl + '/api/weather/' + type
                        + '&north'          + area.north
                        + '&south'          + area.south
                        + '&east'           + area.east
                        + '&west'           + area.west
    ;
    const response = await fetch(url);
    const responseData = await response.json();
    for(var i=0; i<responseData.forecasts.length; i++){
        console.log(responseData.data[i]);
    }
}
```
</details>

#### Get METAR and TAF data for all airports within a specified area

<details>
<summary>
    <code>GET</code> <code><b>/api/metar-taf/area</b></code>
</summary>

##### Parameters:

| name      | type   | required | description                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------|
| north     | number | yes      | Northern latitude of the area in decimal degrees                           |
| south     | number | yes      | Southern latitude of the area in decimal degrees                           |
| east      | number | yes      | Eastern longitude of the area in decimal degrees                           |
| west      | number | yes      | Western longitude of the area in decimal degrees                           |


##### Responses:

| http code     | content-type                      | response               |
|---------------|-----------------------------------|------------------------|
| `200`         | `application/json`                |                        |


##### Example:

```javascript
const baseUrl = "https://weather-data-dev2.atmosoar.io"; 

async function loadMetarTafDataForArea(area) {
    const url = baseUrl + '/api/metar-taf/area' 
                        + '&north'          + area.north
                        + '&south'          + area.south
                        + '&east'           + area.east
                        + '&west'           + area.west
    ;
    const response = await fetch(url);
    const responseData = await response.json();
    console.log(responseData.metarTaf);
}
```
</details>