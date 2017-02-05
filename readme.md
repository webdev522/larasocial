# Reference URL

https://scotch.io/tutorials/laravel-social-authentication-with-socialite

# Requirements

laravel5.2.*

socialite2.*

# Step
## Create developer account for test app

## composer create-project laravel/laravel projectname "5.2.*"

## db config

## user migration update & migrate

[...]

public function up()

    {
    
        Schema::create('users', function (Blueprint $table) {
        
            $table->increments('id');
            
            $table->string('name');
            
            $table->string('email')->nullable();
            
            $table->string('password', 60)->nullable();
            
            $table->string('provider');
            
            $table->string('provider_id')->unique();
            
            $table->rememberToken();
            
            $table->timestamps();
            
        });
        
    }
    
[...]

php artisan migrate

## update user model

[...]

protected $fillable = [

        'name', 'email', 'password', 'provider', 'provider_id'
        
    ];
    
[...]

## make auth

php artisan make:auth

## add socialite

composer require laravel/socialite "2.*"

## update config/app.php

'providers' => [

    // Other service providers...

    Laravel\Socialite\SocialiteServiceProvider::class,
    
],

'aliases' => [

    // Other aliases...

    'Socialite' => Laravel\Socialite\Facades\Socialite::class,
    
],

## update config/services.php

Set the callback URL to http://localhost:8000/auth/twitter/callback

[...]

'twitter' => [

        'client_id'     => env('TWITTER_ID'),
        
        'client_secret' => env('TWITTER_SECRET'),
        
        'redirect'      => env('TWITTER_URL'),
        
    ],
    
[...]

.env

TWITTER_ID={{API Key}}

TWITTER_SECRET={{API secret}}

TWITTER_URL={{callbackurl}}


The FACEBOOK_URL in this case will be http://localhost:8000/auth/facebook/callback

[...]

'facebook' => [

        'client_id'     => env('FACEBOOK_ID'),
        
        'client_secret' => env('FACEBOOK_SECRET'),
        
        'redirect'      => env('FACEBOOK_URL'),
        
    ],
    
[...]


## update routes.php

Route::get('auth/{provider}', 'Auth\AuthController@redirectToProvider');

Route::get('auth/{provider}/callback', 'Auth\AuthController@handleProviderCallback');

## update AuthController.php & register & login blade

# Laravel PHP Framework

[![Build Status](https://travis-ci.org/laravel/framework.svg)](https://travis-ci.org/laravel/framework)
[![Total Downloads](https://poser.pugx.org/laravel/framework/d/total.svg)](https://packagist.org/packages/laravel/framework)
[![Latest Stable Version](https://poser.pugx.org/laravel/framework/v/stable.svg)](https://packagist.org/packages/laravel/framework)
[![Latest Unstable Version](https://poser.pugx.org/laravel/framework/v/unstable.svg)](https://packagist.org/packages/laravel/framework)
[![License](https://poser.pugx.org/laravel/framework/license.svg)](https://packagist.org/packages/laravel/framework)

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable, creative experience to be truly fulfilling. Laravel attempts to take the pain out of development by easing common tasks used in the majority of web projects, such as authentication, routing, sessions, queueing, and caching.

Laravel is accessible, yet powerful, providing tools needed for large, robust applications. A superb inversion of control container, expressive migration system, and tightly integrated unit testing support give you the tools you need to build any application with which you are tasked.

## Official Documentation

Documentation for the framework can be found on the [Laravel website](http://laravel.com/docs).

## Contributing

Thank you for considering contributing to the Laravel framework! The contribution guide can be found in the [Laravel documentation](http://laravel.com/docs/contributions).

## Security Vulnerabilities

If you discover a security vulnerability within Laravel, please send an e-mail to Taylor Otwell at taylor@laravel.com. All security vulnerabilities will be promptly addressed.

## License

The Laravel framework is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).
