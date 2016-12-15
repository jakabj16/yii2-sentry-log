yii2-sentry-log
===============

Yii2 Sentry target for logging based on Raven client.

## Installation

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
$ php composer.phar require jakabj16/yii2-sentry-log "~1.0.0"
```

or add

```
"jakabj16/yii2-sentry-log": "~1.0.0"
```

to the ```require``` section of your `composer.json` file.

## Usage

Add target class in your project config:

```
'components' => [
    'log' => [
        'targets' => [
            [
                'class' => 'sentry\SentryTarget',
                'levels' => ['error', 'warning'],   // or smth else
                'dsn' => '',                        // sentry access string
                'options' => ['release' => 'dev'],  // sentry options
            ],
        ],
    ],
```

Then use like ordinary log:

```
Yii::error('some string');
```

or 

```
Yii::error([
    'msg' => 'some message',
    'data' => [...],                // Any pair key=>value for adding to the sentry message 
]);
```

## Note

Because the mechanism of logging is asyncronical, standard sentry stacktrace is unavailable.
But this extension sends logger stacktrace in extra parameters of message.
