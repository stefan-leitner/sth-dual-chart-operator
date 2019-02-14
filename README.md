Code Example
============

At the moment I'm working on different Widgets and Operators for the Wirecloud Application MashUp-Platform, part of the FIWARE (https://www.fiware.org/) ecosystem. The following operator should serve as code example for my job application.

The purpose of the operator called "sth-dual-chart-operator" is to retrieve historical data for two sensors for a given time range, merge the data and provide a JSON object for Google Charts (Dual-Y LineChart). As shown below the operator serves as link between the input mask and output as Google Charts

The operator recevies as input a JSON object with the follwoing format

```json
{
    "aggregationMethod": "max",
    "aggregationPeriod": "day",
    "attribute1": "airPressure",
    "attribute2": "humidity",
    "datetime": "30. Juli 2018 00:00 - 5. August 2018 23:00",
    "entity1": "Sensor3",
    "entity2": "Sensor6"
}
```
Based on this input the operator creates an url for `entityX` and and `attributeX` to receive the historical data. `datetime`, `aggregationMethod` as well as the `aggregationPeriod` are send as requestParameters.

e.g. `http://pep-comet:8666/STH/v1/contextEntities/type/static/id/Sensor3/attributes/airPressure`.

The received data is processed by the operator and the following JSON output for Google Charts is created.

```json
{
  "type": "LineChart",
  "options": {
    "title": "Maximum pro Tag",
    "series": {
      "0": {
        "targetAxisIndex": 0
      },
      "1": {
        "targetAxisIndex": 1
      }
    },
    "vAxes": {
      "0": {
        "title": "airPressure [hPa]"
      },
      "1": {
        "title": "humidity [%]"
      }
    },
    "hAxis": {
      "title": "Datum und Zeit"
    },
    "pointSize": 1
  },
  "data": [
    [
      "Time",
      "airPressure - Sensor3",
      "humidity - Sensor6"
    ],
    [
      "30.07.18",
      974.04,
      null
    ],
    [
      "31.07.18",
      974.12,
      70.01
    ],
    [
      "01.08.18",
      975.59,
      77.25
    ],
    [
      "02.08.18",
      977.42,
      90.61
    ],
    [
      "03.08.18",
      977.22,
      90.74
    ],
    [
      "04.08.18",
      975.93,
      90.35
    ],
    [
      "05.08.18",
      974.93,
      84.96
    ]
  ]
}

```

