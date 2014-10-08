Installation

Can be installed by using composer

```json
{
  "name": "xkraty/sidekiq-job-pusher",
  "description": "PHP client to interface with Sidekiq",
  "repositories": [
  {
    "type": "package",
    "package": {
      "name": "sidekiq-job-pusher/sidekiq-job-pusher",
      "version": "master",
      "source": {
        "url": "https://github.com/xkraty/sidekiq-job-pusher.git",
        "type": "git",
        "reference": "master"
      }
    }
  }
  ],
  "require": {
    "sidekiq-job-pusher/sidekiq-job-pusher": "dev-master",
    "predis/predis": "0.8.*@dev"
    },
    "autoload": {
      "psr-0": {
        "": "lib/"
      }
    },
    "config": {
      "bin-dir": "bin"
    }
  }
```


Basic usage:

```php
$redis = new Predis\Client();

$sidekiq = new SidekiqJobPusher\Client($redis);

$sidekiq->perform('TestWorker');
```

Advanced usage:

```php
$redis = new Predis\Client(array(
	'host' => 'localhost',
	'port' => '6379',
	'database' => 12,
));

$sidekiq = new SidekiqJobPusher\Client($redis, 'my-namespace');

$args = array('arg1', 'arg2');
$retry = true;
$queue = 'my-queue';

$sidekiq->perform('TestWorker', $args, $retry, $queue);
```
