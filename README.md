# api avito

PHP Фасад для API Avio (www.avito.ru)

#### Схема работы API
https://miro.com/app/board/uXjVKHFfUB0=/

#### Реализация
 - API: реализация запросов к api сервису `Head Hunter`
 - Servcie: Фасад для класса API

### Использование Api
Методы Api возвращают массив с данными.
```php
use and_y87\api_avito\ApiAvito;
use and_y87\api_avito\dto\AvitoApiRequisites;
use and_y87\api_avito\cache\CacheProvider;

// Add `CacheProvider`
class RedisCacheProvider extends CacheProvider
{
    public function getValue( string $key ): string
    {
        return (string) Yii::$app->redis->get( $key );
    }

    public function setValue( string $key, mixed $value ): bool
    {
        return Yii::$app->redis->set( $key, $value );
    }
}

// Create object `CacheProvider`
$redisCacheProvider = new RedisCacheProvider();

// Create object `Requisites`
$avitoApiRequisites = new AvitoApiRequisites( $client_id, $client_secret );

// Create object `Api`
$apiAvito = ApiAvito( $avitoApiRequisites, $redisCacheProvider );

// Use `Api`
$me = $apiAvito->me(); // return array
```
### Использование Service
Методы Service возвращают Объекты с данными.
```php
use and_y87\api_avito\service\AvitoService;

//Вводная часть при использовании сервиса аналогична Api

// Create object `Service`
$avitoService = new AvitoService($apiAvito);

// Use `Service`
$me = $avitoService->me(); // return and_y87\api_avito\response\Me();
```

### Исходная документация API `Avio`: 
 - https://developers.avito.ru/about-api
 - https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.0.md
