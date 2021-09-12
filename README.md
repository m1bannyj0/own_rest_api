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












