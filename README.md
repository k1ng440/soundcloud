# Soundcloud.com API Wrapper
Soundcloud API wrapper written in PHP just for fun.

This piece of code is still in ALPHA.
For now only Authentication over OAuth2 and GET Resources are working.
 
## Requirements
PHP >= 5.3 with cURL support.
 
## Examples

#### Accessing public resources
```php
$soundcloud = new Soundcloud('CLIENT_ID', 'CLIENT_SECRET', 'REDIRECT_URI');

$soundcloud->setResponseType('xml'); // default is json

$response = $soundcloud->getResource('/tracks', array(
                        'q'     => 'House',
                        'order' => 'created_at',
                ));
```

#### Get Authentication URL
```php
$soundcloud = new Soundcloud('CLIENT_ID', 'CLIENT_SECRET', 'REDIRECT_URI');

$authURL = $test->getAuthUrl();
echo '<a href="' . $authURL . '">Login with Soundcloud</a><br>'; 
```

### Get Access Token
```php
...

$accessToken = $test->getAccessToken($_GET['code']);
    
// let's set the token so we can request private resources with getResource() method;
$test->setAccessToken($accessToken->access_token);

// Get User private information
$response = $soundcloud->getResource('/me');
        
// lets keep access token in $_SESSION too, or maybe set it to a database table.. what
// ever fits you best.
$_SESSION['oauth_token'] = $accessToken->access_token;
    }
}
```