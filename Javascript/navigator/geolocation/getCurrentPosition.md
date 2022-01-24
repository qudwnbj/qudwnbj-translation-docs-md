# `navigator.geolocation.getCurrentPosition`

Javascript에서 현재 장치의 위치를 가져오는 API입니다.

```js
navigator.geolocation.getCurrentPosition(
  successCallback,
  errorCallback,
  options
);

//USAGE
navigator.geolocation.getCurrentPosition(
  (position) => {
    console.log(position.coords.latitude);
  },
  (error) => {
    console.log(error.code);
  }
),{ timeout: Infinity, maximumAge: 0, enableHighAccuracty: true });
```

## Parameter

### - `successCallback:(position) => void`

- **Parameter**

| Name                      | Description                                                                                                                                                                                                                                                                                                                 | Type                   |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| `coords`                  | 시간과 위치를 나타내는 객체입니다.                                                                                                                                                                                                                                                                                          | Object                 |
| `coords.latitude`         | 십진수로 위치의 위도를 나타내는 double을 반환합니다.                                                                                                                                                                                                                                                                        | number(double)         |
| `coords.longitude`        | 십진수로 위치의 경도를 나타내는 double을 반환합니다.                                                                                                                                                                                                                                                                        | number(double)         |
| `coords.altitude`         | 해수면을 기준으로 위치의 고도를 미터 단위로 나타내는 double을 반환합니다. 구현에서 데이터를 제공할 수 없는 경우 이 값은 null일 수 있습니다.                                                                                                                                                                                 | number(double) \| null |
| `coords.accuracy`         | 미터로 표시되는 위도 및 경도 속성의 정확도를 나타내는 double을 반환합니다.                                                                                                                                                                                                                                                  | number(double)         |
| `coords.altitudeAccuracy` | 미터로 표시된 고도의 정확도를 나타내는 double을 반환합니다. 이 값은 null일 수 있습니다.                                                                                                                                                                                                                                     | number(double) \| null |
| `coords.heading`          | 장치가 향하고 있는 방향을 나타내는 double을 반환합니다. 도 단위로 지정된 이 값은 장치가 진북 방향에서 얼마나 멀리 떨어져 있는지 나타냅니다. 0도는 진북을 나타내며 방향은 시계 방향으로 결정됩니다(즉, 동쪽은 90도, 서쪽은 270도). 속도가 0이면 헤딩은 NaN입니다. 장치가 표제 정보를 제공할 수 없는 경우 이 값은 null입니다. | number(double) \| null |
| `coords.speed`            | 초당 미터 단위로 장치의 속도를 나타내는 double을 반환합니다. 이 값은 null일 수 있습니다.                                                                                                                                                                                                                                    | number(double) \| null |
| `timestamp`               | 현재 시간을 timestamp로 반환합니다.                                                                                                                                                                                                                                                                                         | number(long)           |

### - `errorCallback:(error) => void`

- **Parameter**

| Name      | Description                                                         | Type        |
| --------- | ------------------------------------------------------------------- | ----------- |
| `code`    | 에러 코드 1: PERMISSION_DENIED, 2: POSITION_UNAVAILAVLE, 3: TIMEOUT | 1 \| 2 \| 3 |
| `message` | 에러메세지                                                          | string      |

### - `options`

| Name                 | Description                                                                                                                                                                                                                                                                                                                                    | Type         |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| `timeout`            | 기가 위치를 반환할 때 소모할 수 있는 최대 시간(밀리초)을 나타내는 양의 long 값입니다. 기본 값은 Infinity로, 위치를 알아내기 전에는 getCurrentPosition()이 반환하지 않을 것임을 나타냅니다.                                                                                                                                                     | number(long) |
| `maximumAge`         | 캐시에 저장한 위치정보를 대신 반환할 수 있는 최대 시간을 나타내는 양의 long 값입니다. 0을 지정한 경우 장치가 위치정보 캐시를 사용할 수 없으며 반드시 실시간으로 위치를 알아내려 시도해야 한다는 뜻입니다.Infinity를 지정한 경우 지난 시간에 상관없이 항상 캐시에 저장된 위치정보를 반환해야 함을 나타냅니다. 기본 값은 0입니다.                | number(long) |
| `enableHighAccuracy` | 위치정보를 가장 높은 정확도로 수신하고 싶음을 나타내는 불리언 값입니다.true를 지정했으면, 지원하는 경우 장치가 더 정확한 위치를 제공합니다.그러나 응답 속도가 느려지며 전력 소모량이 증가하는 점에 주의해야 합니다.반면 false를 지정한 경우 기기가 더 빠르게 반응하고 전력 소모도 줄일 수 있는 대신 정확도가 떨어집니다.기본 값은 false입니다. | boolean      |
