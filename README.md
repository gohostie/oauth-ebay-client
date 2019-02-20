# oauth-ebay-client
oauth-ebay-client

# Install
composer require gohostie/oauthebay-client

# Usage
$provider = new \NeilCrookes\OAuth2\Client\Provider\Ebay([
    'clientId' => 'YOUR EBAY APP ID',
    'clientSecret' => 'YOUR EBAY CERTIFICATE ID',
    'redirectUri' => 'YOUR EBAY "RU" NAME',
    'scopeSeparator' => ' ',
    'sandbox' => true, //defaults to false, i.e. production
    'http_errors' => false, // Optional. Means Guzzle Exceptions aren't thrown on 4xx or 5xx responses from eBay, allowing you to detect and handle them yourself
], [
    'optionProvider' => new \League\OAuth2\Client\OptionProvider\HttpBasicAuthOptionProvider()
]);

$accessToken = $provider->getAccessToken('authorization_code', [
    'code' => $_GET['code']
]);

$ebayUser = $provider->getResourceOwner($accessToken);

echo $ebayUser->getId(); // eBay User's user id
echo $ebayUser->getEmail(); // eBay User's email address
