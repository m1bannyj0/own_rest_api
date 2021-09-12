1. Маршрут /api настроен API-платформой и может редактироваться из файла /config/routes/api_platform.yaml

        ./bin/console debug:router

2. Откройте .envфайл, расположенный в корне проекта, и обновите DATABASE_URL

       ./bin/console doctrine:database:create

3. Kонечные точки API

        symfony console make:entity Superheroes

        # To check the raw sql query before executing
        ./bin/console doctrine:schema:update --dump-sql

        # To execute the SQL query
        ./bin/console doctrine:schema:update --force
        # output: [OK] Database schema updated successfully! 

4. http://127.0.0.1:8000/api/superheroes?page=1

5. Исключение свойств из конечной точки API.

   _сделаем created_atсвойство необязательным_

Меняем [аннотации в файле](https://github.com/mrbannyjo/own_rest_api/commit/84666869a5133195f3f0de7766168224e295c9b1#diff-8640ee24046ea404387259cedf6cb9a3c29b46427a2bb7f7dec90e4b75054e30R52)

Это может пока не сработать, потому что мы используем аннотации, и для этого нам нужно разрешить их использование с
сериализатором Symfony.

      # config/packages/framework.yaml
      framework:
         serializer: { enable_annotations: true }

      # update doctrine/annotations to the latest version
      composer req doctrine/annotations

Как и ожидалось, created_atсвойство отсутствует, поскольку стало доступным только для чтения.

_Примечание . Если у вас есть проблемы с отображением этой страницы, убедитесь, что вы обновили кеш._

      # refresh cache
      php bin/console cache:clear --no-warmup --env=dev
      php bin/console cache:warmup --env=dev

6. Добавление префикса маршрута

   Добавить префикс маршрута довольно просто. Все, что вам нужно сделать, это добавить правильную аннотацию. Следуя
   примеру **src/Entity/media.php**, мы добавили атрибут, "route_prefix"="/dc"

      @ApiResource(
         attributes={"route_prefix"="/dc"},





