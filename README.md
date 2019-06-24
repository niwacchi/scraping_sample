# Scraping sample by Laravel, Goutte.
## Preparing
1. Install Laravel for global.
    ```sh
    composer global require laravel/installer
    ```
1. Create project.
    ```sh
    laravel new scraping_sample
    ```
1. Getting Goutte.
    ```sh
    composer require weidner/goutte
    ```
## Coding
### config/app.php
- Add provider.
```php
'provider' -> [
    Weidner\Goutte\GoutteServiceProvider::class,
]
```
- Add alias.
```php
'alias' -> [
    'Goutte' => Weidner\Goutte\GoutteFacade::class,
]
```
### Create command.
```sh
php artisan make:command Scraping
```
### app/Console/Commands/Scraping
```php
protected $signature = 'command:scraping';
```
- access niwacchi.net, and get top page url link list.
```php
public function handle()
{
    $goutte = GoutteFacade::request('GET', 'https://niwacchi.net');
    $goutte->filter('.content')->each(function ($content) {
        echo $content->filter('a')->attr('href') . "\n";
    });
}
```
## Execute scraping
```sh
php artisan command:scraping
```