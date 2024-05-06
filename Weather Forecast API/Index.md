# Weather Forecast API

[Home](../README.md)・Weather Forecast API

## Endpoints

### Base URL

`https://weather-data-eu.atmosoar.io`

#### Get weather forecast for a specified point and time

<details>
<summary>
    <code>GET</code> <code><b>/api/forecast/get-point-forecast</b></code>
</summary>

##### Parameters:

| name      | type   | required | description                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------|
| latitude  | number | yes      | Latitude of the point in decimal degrees                                   |
| longitude | number | yes      | Longitude of the point in decimal degrees                                  |
| datetime  | string | yes      | Date and Time of the forecast (ISO format, example: `2022-12-31T12:30:15`) |


##### Responses:

| http code     | content-type                      | response               |
|---------------|-----------------------------------|------------------------|
| `200`         | `application/json`                |                        |


##### Example:

```javascript
const baseUrl = "https://weather-data-eu.atmosoar.io";
const authKey = "YOUR_API_KEY"

async function loadForecastData(point, datetime) {
    const url = baseUrl + '/api/forecast/get-point-forecast'
                        + '?key'            + authKey
                        + '&latitude'       + point.latitude
                        + '&longitude'      + point.longitude
                        + '&datetime'       + datetime.toISOString()
    ;
    const response = await fetch(url);
    const responseData = await response.json();
    console.log(responseData.forecast);
}
```
</details>

#### Get weather forecast for a specified area and time

<details>
<summary>
    <code>GET</code> <code><b>/api/forecast/get-area-forecast</b></code>
</summary>

##### Parameters:

| name      | type   | required | description                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------|
| north     | number | yes      | Northern latitude of the area in decimal degrees                           |
| south     | number | yes      | Southern latitude of the area in decimal degrees                           |
| east      | number | yes      | Eastern longitude of the area in decimal degrees                           |
| west      | number | yes      | Western longitude of the area in decimal degrees                           |
| datetime  | string | yes      | Date and Time of the forecast (ISO format, example: `2022-12-31T12:30:15`) |


##### Responses:

| http code     | content-type                      | response               |
|---------------|-----------------------------------|------------------------|
| `200`         | `application/json`                |                        |


##### Example:

```javascript
const baseUrl = "https://weather-data-eu.atmosoar.io";
const authKey = "YOUR_API_KEY"

async function loadForecastData(area, datetime) {
    const url = baseUrl + '/api/forecast/get-area-forecast'
                        + '?key'            + authKey
                        + '&north'          + area.north
                        + '&south'          + area.south
                        + '&east'           + area.east
                        + '&west'           + area.west
                        + '&datetime'       + datetime.toISOString()
    ;
    const response = await fetch(url);
    const responseData = await response.json();
    for(var i=0; i<responseData.forecasts.length; i++){
        console.log(responseData.forecasts[i]);
    }
}
```
</details>

## Units and Conventions