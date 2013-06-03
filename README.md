# Reddit Notify

This console script simply e-mail notifys a Reddit user that they have an inbox (comment or priv message). It can be setup to run for one or multiple accounts.

I built this because I use Alien Blue for iOS and it does not do push notifications, I figured this would be a good solution, hope it helps others!

## Fetch

The recommended way to install this script is [through composer](http://packagist.org).

Just create a composer.json file for your project:

```JSON
{
    "minimum-stability" : "dev",
    "require": {
        "tyler-king/reddit-notify": "dev-master"
    }
}
```

And run these two commands to install it:

    $ curl -s http://getcomposer.org/installer | php
    $ php composer.phar install

## Setup

Modify `data/reddit-notify.yml` and input your mailer settings.

## Usage

Execute the `reddit-notify check` command.

```bash
$ bin/reddit-notify check --username=your_reddit_username --passwd=your_reddit_password
```

This will check your unread messages and e-mail you a descriptive e-mail about the comment or message. It will not re-notify you, it will record the last message ID checked and then check again from there on next run.

Subject message format is as followed: `[RN] {TYPE: Private|Comment}: {USER} - {SUBJECT LINE}`

## Cron Install

Of course you want this running in the background checking, so on your server, run `crontab -e` and add the following for a check every 15 minutes:

```bash
*/15 * * * * /usr/bin/php {path_to_your_clone}/bin/reddit-notify check --username=your_reddit_username --passwd=your_reddit_password
```

Again you may set this up for multiple accounts as such:

```bash
*/15 * * * * /usr/bin/php {path_to_your_clone}/bin/reddit-notify check --username=your_reddit_username --passwd=your_reddit_password
*/15 * * * * /usr/bin/php {path_to_your_clone}/bin/reddit-notify check --username=your_reddit_username2 --passwd=your_reddit_password2
```

By adding the `--config` option you may supply different mailer setup configs for each account.

## Options

```bash
vendor/bin/reddit-notify check --help
Usage:
 check [--username="..."] [--passwd="..."] [--config="..."]

Options:
 --username            Reddit username
 --passwd              Reddit passwd
 --config              Configuration path
 --help (-h)           Display this help message.
 --quiet (-q)          Do not output any message.
 --verbose (-v)        Increase verbosity of messages.
 --version (-V)        Display this application version.
 --ansi                Force ANSI output.
 --no-ansi             Disable ANSI output.
 --no-interaction (-n) Do not ask any interactive question.
```

## Example

![Screenshot](https://raw.github.com/tyler-king/reddit-notify/master/ios.jpg "Screenshot")
![Screenshot](https://raw.github.com/tyler-king/reddit-notify/master/thunderbird.jpg "Screenshot")