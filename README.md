## Узнать погоду в любом городе на Python
Для получения сводки о погоде в любом городе можно использовать API (Application Programming Interface) от различных сервисов, например, OpenWeatherMap. Для использования этого API необходимо зарегистрироваться на их сайте и получить API ключ.

Ниже приведен пример кода на Python, который использует API от OpenWeatherMap для получения сводки о погоде в заданном городе:


```Python
import requests

api_key = 'your_api_key_here'
city = input('Enter city name: ')

url = f'http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}'

response = requests.get(url)

if response.status_code == 200:
    data = response.json()
    weather = data['weather'][0]['main']
    temperature = round(data['main']['temp'] - 273.15, 1)
    feels_like = round(data['main']['feels_like'] - 273.15, 1)
    humidity = data['main']['humidity']
    wind_speed = data['wind']['speed']

    print(f'Weather in {city}: {weather}')
    print(f'Temperature: {temperature} °C')
    print(f'Feels like: {feels_like} °C')
    print(f'Humidity: {humidity}%')
    print(f'Wind speed: {wind_speed} m/s')
else:
    print('Error occurred while retrieving weather data')  
```
Данный код запрашивает у пользователя название города, затем использует API от OpenWeatherMap для получения данных о погоде в заданном городе. Если запрос выполнен успешно (HTTP-код ответа 200), то выводится сводка о погоде, в противном случае выводится сообщение об ошибке. Выводится основной тип погоды, температура в градусах Цельсия, ощущаемая температура, влажность и скорость ветра.

Обратите внимание, что данный код выводит только основные параметры погоды. Чтобы получить более подробную информацию о погоде в заданном городе, необходимо использовать соответствующие параметры API и обработать соответствующие данные в коде.

Для добавления возможности получить сводку о погоде еще раз, можно поместить код для получения погоды в цикл while и предложить пользователю повторно ввести название города. Вот пример кода с добавлением этой функциональности:

```Python
import requests

api_key = 'your_api_key_here'

while True:
    city = input('Enter city name (or "exit" to quit): ')
    
    if city.lower() == 'exit':
        break
    
    url = f'http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}'

    response = requests.get(url)

    if response.status_code == 200:
        data = response.json()
        weather = data['weather'][0]['main']
        temperature = round(data['main']['temp'] - 273.15, 1)
        feels_like = round(data['main']['feels_like'] - 273.15, 1)
        humidity = data['main']['humidity']
        wind_speed = data['wind']['speed']

        print(f'Weather in {city}: {weather}')
        print(f'Temperature: {temperature} °C')
        print(f'Feels like: {feels_like} °C')
        print(f'Humidity: {humidity}%')
        print(f'Wind speed: {wind_speed} m/s')
    else:
        print('Error occurred while retrieving weather data')

```
Этот код использует цикл while True, чтобы продолжать запрашивать у пользователя названия городов до тех пор, пока пользователь не введет "exit". Когда пользователь вводит название города, выполняется запрос к API OpenWeatherMap и выводится сводка о погоде в этом городе. Затем цикл продолжается и пользователь снова может ввести название города или ввести "exit", чтобы завершить программу.