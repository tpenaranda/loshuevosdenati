# Los Huevos de Nati
A fancy responsive form to buy customized easter eggs and an admin panel to have a look to orders placed. Laravel & VueJS.

<p align="center">
  <img src="https://raw.githubusercontent.com/tpenaranda/loshuevosdenati/master/screenshot.png" alt="App screenshot"/>
</p>

## Requirements

* PHP >= 7.1.3
    * BCMath PHP Extension
    * Ctype PHP Extension
    * JSON PHP Extension
    * Mbstring PHP Extension
    * OpenSSL PHP Extension
    * PDO PHP Extension
    * Tokenizer PHP Extension
    * XML PHP Extension
* Composer
* MySQL
* Redis
* npm

## Install

1. `git clone https://github.com/tpenaranda/loshuevosdenati`

2. Create empty mysql database.

3. Rename `.env.example` file to `.env` and configure DB and Redis values

4. `composer update`

5. `php artisan migrate --seed`

6. `php artisan key:generate`

7. `npm install`

8. `npm run dev`

9. `php artisan serve` to start dev server.

## Tests (PHP SQLite driver required)
`vendor/phpunit/phpunit/phpunit`
