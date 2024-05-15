# api avito

PHP Фасад для API Avio (www.avito.ru)

#### Схема работы API
https://miro.com/app/board/uXjVKHFfUB0=/

#### Реализация
 - API: реализация запросов к api сервису `Head Hunter`
 - Servcie: Фасад для класса API

### Использование Api
```php
use and_y87/api_avito/ApiAvito;
use and_y87/api_avito/dto/AvitoApiRequisites;
use and_y87/api_avito/tools/CacheProvider;

// Add `CacheProvider`
class RedisCacheProvider extends CacheProvider
{
    public function getValue(string $key )
    {
        Yii::$app->redis->get( $key );
    }

    public function setValue( string $key, string $value )
    {
        Yii::$app->redis->set( $key, value );
    }
}

// Create object `CacheProvider`
$redisCacheProvider = new RedisCacheProvider();

// Create object `Requisites`
$avitoApiRequisites = new AvitoApiRequisites( $client_id, $client_secret );

// Create object `Api`
$apiAvito = ApiAvito( $avitoApiRequisites, $redisCacheProvider );

// Use `Api`
```

### Исходная документация API `Avio`: 
 - https://developers.avito.ru/about-api
 - https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.0.md
