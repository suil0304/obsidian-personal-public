> [!note]+ # #8.0 Geolocation
> 날씨를 구현하기 위해 /js 안에 weather.js를 생성하다
> 
> 이제부터 새로운 것들을 사용해볼 예정인
> 
> ```javascript
> navigator.geolocation.getCurrentPosition();
> ```
> 
> 그러하구요
> 
> 안에는 인자가 1개 필요하다고 나와 있구요
> 흐음
> 
> ![[image 160.png]]
> 
> successCallback을 넣어야 했구요
> 흐음
> 
> ```javascript
> /**
>  * @type {PositionCallback}
>  */
> function geoSuccess(position) {
>     console.log(position);
> }
> /**
>  * @type {PositionErrorCallback}
>  */
> function geoError(positionError) {
> 
> }
> 
> navigator.geolocation.getCurrentPosition(geoSuccess, geoError);
> ```
> 
> 이렇게 하면 꽤나 편리하구요
> 크하하
> 
> ```javascript
> /**
>  * @type {PositionErrorCallback}
>  */
> function geoError(positionError) {
>     alert("Can't find geolocation.");
> }
> ```
> 
> 무언가 이상이 생겼다면 못 가져온다는 뜻이니 alert로 안내해주도록 하구요
> 이러언
> 
> 대충 이러언을 읽어보면
> geoSuccess에는 GeolocationPosition 객체가 들어가구요
> 
> position.coords.latitude는 위도
> position.coords.longitude는 경도구요
> 
> 이제 Weather API를 사용하기 위해 [openweathermap.org](http://openweathermap.org/)로 가서 API key를 발급 받아야 하구요
> 익숙하잖아용
> 이러언
> 
> 다 만들었으면 다음에 합시다
> 이러언

> [!note]+ # #8.1 Weather API
> 그래서 Current Weather Data라는 API를 사용해볼 수 있겠구요
> API를 넣고 위도와 경도를 넣고 내리면???
> 말 그대로 현재의 데이터가 나오구요
> 
> ![[image 161.png]]
> 
> 이것을 보는데
> temp가 아무리 봐도 이상하죠???
> 
> 화씨인 것 같구요
> 섭씨로 변경하려면 다음과 같은 수식을 적용시켜야 할 필요가 있었으나
> 
> $$
> °C = (°F-32)\times\frac{5}{9}
> $$
> 
> [Current weather data](https://openweathermap.org/api/current?collection=current_forecast)을 읽어보면 unit을 같이 보내어 이러언할 수 있었구요
> 호오
> 
> ![[image 162.png]]
> 
> 이제는 다음과 같이 섭씨 온도로 나오고 있네용
> 이-히히
> 
> 이제 weather id를 가진 div 요소를 HTML에 추가하다
> 
> ```html
> <div id="weather">
>     <span></span>
>     <span></span>
> </div>
> ```
> 
> ```javascript
> /**
>  * @typedef {{
>  *      coord:{
>  *          lat:number,
>  *          lon:number
>  *      };
>  *      weather:{
>  *          id:number,
>  *          main:string,
>  *          description:string,
>  *          icon:string
>  *      }[];
>  *      base:string;
>  *      main:{
>  *          temp:number,
>  *          feels_like:number,
>  *          temp_min:number,
>  *          temp_max:number,
>  *          presure:number,
>  *          humidity:number,
>  *          sea_level:number,
>  *          grnd_level:number
>  *      };
>  *      visibility:number;
>  *      wind:{
>  *          speed:number,
>  *          deg:number,
>  *          gust?:number
>  *      };
>  *      clouds: {
>  *          all:number
>  *      };
>  *      dt:number;
>  *      sys:{
>  *          country:string,
>  *          sunrise:number,
>  *          sunset:number
>  *      };
>  *      timezone:number;
>  *      id:number;
>  *      name:string;
>  *      cod:number;
>  * }} WeatherData
>  */
> 
> /**
>  * 
>  * @param {number} lat 
>  * @param {number} lng 
>  * @returns {Promise<WeatherData>}
>  */
> async function getCurrentWeatherData(lat, lng) {
>     return fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lng}&appid=${WEATHER_API_KEY}&units=metric`)
>         .then((res) => {
>             return res.json();
>         })
>         .catch((error) => {
>             console.error(error);
>         });
> }
> 
> /**
>  * @type {PositionCallback}
>  */
> function geoSuccess(position) {
>     const lat = position.coords.latitude;
>     const lng = position.coords.longitude;
> 
>     (async () => {
>         const data = await getCurrentWeatherData(lat, lng);
> 
>         const weather = document.getElementById("weather-text");
>         const city = document.getElementById("city-text");
> 
>         weather.innerText = data.weather[0].main;
>         city.innerText = data.name;
>     })();
> }
> ```
> 
> 이렇게 할 수 있겠구요
> 
> 온도도 추가해보다
> 
> ```javascript
> weather.innerText = `${data.weather[0].main} / ${data.main.temp}`;
> ```
> 
> ![[image 163.png]]
> 
> 아주좋았어

> [!note]+ # #8.2 Conclusions
> 끝났구요
> 
> 만약 더 하고 싶다면???
> 
> [nomadcoders.co/wetube](http://nomadcoders.co/wetube)을 참조하면 될 것 같구요
> 이러언