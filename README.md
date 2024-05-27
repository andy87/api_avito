# providerAvito

PHP Фасад для API Avio (www.avito.ru)

---

> [!NOTE]
> ![IN PROGRESS](http://www.bc-energy.it/wp-content/uploads/2013/08/work-in-progress.png)

---

#### Реализация
 - API: реализация запросов к api сервису `Avito`
 - Servcie: Фасад для класса API

### Использование Api
Методы Api возвращают массив с данными.
```php
use and_y87\api_avito\ApiAvito;
use and_y87\api_avito\dto\AvitoApiRequisites;
use and_y87\api_avito\cache\CacheProvider;

// Создание класса `CacheProvider`
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

// Создание экземпляра класса `CacheProvider`
$redisCacheProvider = new RedisCacheProvider();

// Создание экземпляра класса `Requisites`
$avitoApiRequisites = new AvitoApiRequisites( $client_id, $client_secret );

// Создание экземпляра класса `Api`
$apiAvito = ApiAvito( $avitoApiRequisites, $redisCacheProvider );

// Использование `Api`
$me = $apiAvito->me(); // return array

echo $me['name']; // получение значения массива по ключу (hardcode)
```
### Использование Service
Методы Service возвращают объекты(экзмпляры классов) содержащие актуальные для endpoint свойства, согласно документации сервиса.
```php
use and_y87\api_avito\service\AvitoService;

//Вводная часть при использовании сервиса аналогична Api

// Создание экземпляра класса `Service`
$avitoService = new AvitoService($apiAvito);

// Использование `Service`
$me = $avitoService->myInfo(); // return and_y87\api_avito\response\Me();

echo $me->name; // Получение значение из объекта через обращение к свойству
```

#### Схема работы API
![Схема работы API](https://static.andy87.ru/github/api/apiLogivSchema.png?v=3)

### Исходная документация API `Avio`: 
 - https://developers.avito.ru/about-api
 - https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.0.md
