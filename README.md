EbayApiBundle
=============

This project intends to create a simple wrapper around main eBay APIs:

* Shopping
* Finding
* Trading

**Caution:** Calls for Trading API are in progress... Coming soon.

API Reference (supporting calls)
--------------------------------

* Shopping API (version 897)
    * FindHalfProducts
    * FindPopularItems
    * FindPopularSearches
    * FindProducts
    * FindReviewsAndGuides
    * GetCategoryInfo
    * GeteBayTime
    * GetItemStatus
    * GetMultipleItems
    * GetShippingCosts
    * GetSingleItem
    * GetUserProfile

* Finding API (version 1.13.0)    
    * findCompletedItems
    * findItemsAdvanced
    * findItemsByCategory
    * findItemsByImage **Caution:** temporary not Supporting!
    * findItemsByKeywords
    * findItemsByProduct
    * findItemsIneBayStores
    * getHistograms
    * getSearchKeywordsRecommendation
    * getVersion

* Trading API (version 903)
    * GetCategories
    * **Caution:** Other calls are in progress...

Simple example
-------------

(in controller):

```php
$api = 'Shopping';
$callName = 'GetSingleItem';
$ebay = $this->get('web_consul_ebay_api.main');
$call = $ebay->getInstance('Shopping', 'GetSingleItem', $ebay::MODE_PRODUCT);
$variationSpecifics = [];
$nameValueList = new NameValueList();
$nameValueList->setName('Colour')->setValue(['RED']);
$variationSpecifics[] = $nameValueList;
// set Call-specific and  Standard Input Fields
$call
     ->setItemID(151551119370)
     ->setIncludeSelector('Details, Variations')
     ->setVariationSpecifics($variationSpecifics);
// get response in XML format     
$service = $this->get('web_consul_ebay_api.make_call');
$output = $service->getResponse($call);
```

Full documentation will be stored in the `Resources/doc/index.md`

Installation
------------
#### Step 1: Download EbayApiBundle using composer
Add EbayApiBundle in your composer.json:
```js
{
    "require": {
        "webconsul/ebay-api-bundle": "0.2.*"
    }
}
```
#### Step 2: Update composer
``` bash
$ php composer.phar update webconsul/ebay-api-bundle
```
### Step 3: Enable the bundle

``` php
<?php
// app/AppKernel.php
public function registerBundles()
{
    $bundles = array(
        // ...
        new WebConsul\EbayApiBundle\WebConsulEbayApiBundle(),
    );
}
```
### Step 4: Configure
For security reason all configuration parameters of the bundle must be added into `parameters.yml`:
```
parameters:
   ...
   web_consul_ebay_api:
      auth_token: 'YOUR TOKEN FOR TESTING API CALLS'
      application_keys:
        sandbox:
          dev_id: '...'
          app_id: '...'
          cert_id: '...'
        production:
          dev_id: '...'
          app_id: '...'
          cert_id: '...'
```
Values for that parameters you can get on your account page of [the eBay Developers program] (https://developer.ebay.com/DevZone/account/Default.aspx)

All the installation instructions are located in  the documentation.

Examples of the API calls
-----------------
If you want see examples and test API calls, you can configure `CallController` from the EbayApiBundle.
### Step 1: Routing
```js
// app/config/routing.yml
web_consul_ebay_api_homepage:
    resource: "@WebConsulEbayApiBundle/Controller/"
    type: annotation
```
### Step 2: Browsing
Open in your browser: `http://YOUR_HOST/callReference`.

On that page you can see full list of the available API calls.
### Step 3: Change call parameters
You can change parameters for API calls' examples. Just edit `testCallAction` in the `Controller/CallController`.
License
-------
This bundle is under the MIT license. See the complete license in the bundle:

    Resources/meta/LICENSE

Reporting an issue or a feature request
---------------------------------------

Issues and feature requests are tracked in the [Github issue tracker](https://github.com/WebConsul/EbayApiBundle/issues).