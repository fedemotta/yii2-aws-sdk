AWS SDK for Yii2 - Use Amazon Web Services in your Yii2 project
===============================================================
This extension provides the AWS SDK 3 integration for the Yii2 framework

[![Latest Stable Version](https://poser.pugx.org/fedemotta/yii2-aws-sdk/v/stable)](https://packagist.org/packages/fedemotta/yii2-aws-sdk) [![Total Downloads](https://poser.pugx.org/fedemotta/yii2-aws-sdk/downloads)](https://packagist.org/packages/fedemotta/yii2-aws-sdk) [![Latest Unstable Version](https://poser.pugx.org/fedemotta/yii2-aws-sdk/v/unstable)](https://packagist.org/packages/fedemotta/yii2-aws-sdk) [![License](https://poser.pugx.org/fedemotta/yii2-aws-sdk/license)](https://packagist.org/packages/fedemotta/yii2-aws-sdk)

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist fedemotta/yii2-aws-sdk "*"
```

or add

```
"fedemotta/yii2-aws-sdk": "*"
```

to the require section of your `composer.json` file.

```
Note: You can still use AWS version 2 if you specify fedemotta/yii2-aws-sdk "1.*"
```

Usage
-----

To use this extension, simply add the following code in your application configuration:

```php
return [
    //....
    'components' => [
        'awssdk' => [
            'class' => 'fedemotta\awssdk\AwsSdk',
            'credentials' => [
                'key' => 'your-aws-key',
                'secret' => 'your-aws-secret',
            ],
            'region' => 'your-aws-region', //i.e.: 'us-east-1'
            'version' => 'your-aws-version', //i.e.: 'latest'
        ],
    ],
];
```

Getting all balancer names from AWS:

```php
$awssdk = Yii::$app->awssdk->getAwsSdk();
$elb = $awssdk->createElasticloadbalancing();
$load_balancers = $elb->describeLoadBalancers()->toArray();
if (isset($load_balancers['LoadBalancerDescriptions'])){
    foreach ($load_balancers['LoadBalancerDescriptions'] as $balancer){
        if (isset($balancer['LoadBalancerName'])){ 
            echo $balancer['LoadBalancerName'];
        }
    }
}
```
