# Add easy login function during development

When we are developing a laravel app, we might need to enter email + password combination to login to our system during
development stage and that may make developer himself to be annoyed.

This package can help you to overcome those problems by providing the following component.

```blade
    <x-dev-login identifier="someone@somewhere.com"/>
```

Once the user click the button generated by the x-dev-login component, you are authenticated as your desired user
account.

You can also pass attributes to the components as following.

```blade
    <x-dev-login 
        identifier="heidi.connelly@example.net"
        identifier-column="email" 
        redirect-url="{{route('home')}}"
        label="Login as heidi"
        guard="web"
        class="bg-primary"
    />
```

The definitions of the component attributes are as follows.

- identifier - value to be used to be authenticated (mostly user email)
- identifier-column - mysql column to be validated with identifier mentioned above.
- redirect-url - url to be redirected after authenticating the user
- label - label to show on button
- guard - guard to be used when trying to authenticate
- class - class for the component blade

# Note

All the attributes listed above are optional and the very first user in the table will be used to be authenticated by
default if no attribute is passed.

## Installation

You can install the package via composer.

```bash
composer require naythukhant/laravel-dev-login
```

Optionally, you can publish the config file with:

```bash
php artisan vendor:publish --tag="dev-login"
```

Here is how to override the package.

```php
<?php

use NayThuKhant\LaravelDevLogin\Http\Controllers\DevLoginController;

/*all the config are not getting from Env helper since this application should not be messing up the env file*/

return [
    /*default route name to be redirected after logging in*/
    "redirect_route_name" => null,

    /*controller for handling the request,
     invoke function of this controller will be called by default*/
    "login_controller" => DevLoginController::class,

    /*default guard for authentication
    this guard is really important because it works together with application authentication config*/
    "guard" => "web",

    /*default model to authenticate*/
    "auth_model" => null,

    /*this middleware will be applied for the dev login route*/
    "middleware" => 'web',

    /*this will define when to include things provided by this package to be included*/
    "allowed_environments" => ['local']
];

```
