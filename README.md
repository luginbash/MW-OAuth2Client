# MediaWiki OAuth2 Client
MediaWiki implementation of the PHP League's [OAuth2 Client](https://github.com/thephpleague/oauth2-client), to allow MediaWiki to act as a client to any OAuth2 server. Currently maintained by [Schine GmbH](https://www.star-made.org/).

Requires MediaWiki 1.25+.

## Installation

Clone this repo into the extension directory. In the cloned directory, run 'git submodule update --init' to initialize the local configuration file and fetch all data from the OAuth2 client library.

Finally, run [composer](https://getcomposer.org/) in ./vendors/oauth2-client to install the library dependency.

```bash
cd extensions
git clone https://github.com/luginbash/MW-OAuth2Client
cd MW-OAuth2Client
git submodule update --init
composer install
```

## Usage

Add the following line to your LocalSettings.php file.

```php
wfLoadExtension( 'MW-OAuth2Client' );
```

Required settings:

```php
$wgOAuth2Client['client']['id']     = '';
$wgOAuth2Client['client']['secret'] = '';

/*  Example:
 *  authorize_endpoint: https://api.example.net/oauth2/authorize
 *  access_token_endpoint:  https://api.example.net/oauth2/token
 *  api_endpoint:  https://api.example.net/oauth2/userinfo
 *  redirect_uri: http://your.wiki.domain/wiki/Special:OAuth2Client/callback
 */

$wgOAuth2Client['configuration']['authorize_endpoint']     = ''; 
$wgOAuth2Client['configuration']['access_token_endpoint']  = '';
$wgOAuth2Client['configuration']['api_endpoint']           = '';
$wgOAuth2Client['configuration']['redirect_uri']           = ''; 

$wgOAuth2Client['configuration']['username']       = 'username';  
$wgOAuth2Client['configuration']['email']          = 'email'; 
$wgOAuth2Client['configuration']['realname']       = 'realname';  
$wgOAuth2Client['configuration']['scopes']         = 'openid';
```

The **Redirect URI** for your wiki should be and constistent with the one on your provider:

```
http://your.wiki.domain/path/to/wiki/Special:OAuth2Client/callback
```

If you are using Azure AD then it's required to use `openid` as scope. 

Optional further configuration

```php
$wgOAuth2Client['configuration']['http_bearer_token'] = 'Bearer'; // Token to use in HTTP Authentication
$wgOAuth2Client['configuration']['query_parameter_token'] = 'auth_token'; // query parameter to use

$wgOAuth2Client['configuration']['service_name'] = 'Citizen Registry'; // the name of your service
$wgOAuth2Client['configuration']['service_login_link_text'] = 'Login with StarMade'; // the text of the login link

// remove @example.net part from the username, do not use with a multi-tenant provider 
$wgOAuth2Client['configuration']['use_local_part'] = True; 
```

### Popup Window
To use a popup window to login to the external OAuth2 server, copy the JS from modal.js to the [MediaWiki:Common.js](https://www.mediawiki.org/wiki/Manual:Interface/JavaScript) page on your wiki.

### Extension page
https://www.mediawiki.org/wiki/Extension:OAuth2_Client

## License
LGPL (GNU Lesser General Public License) http://www.gnu.org/licenses/lgpl.html
