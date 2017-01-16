# GoCardless Direct Debit integration for CiviCRM

**A CiviCRM extension to GoCardless integration to handle UK 
Direct Debits.**

A better readme is to come :-)

Meanwhile pre-launch, please see and use the issue queue, especially 
see [#1](https://github.com/artfulrobot/uk.artfulrobot.civicrm.gocardless/issues/1) which sets out the urgent project goals. I will be launching 
with basic functionality by mid November.


## How you can help

I'd welcome your input. Please note that this extension is **NOT 
production-ready yet**.

Let me know - see [#7](https://github.com/artfulrobot/uk.artfulrobot.civicrm.gocardless/issues/7)

Note: if you're running a "test-drive" contribution page you can use GoCardless's test bank account: 20-00-00 55779911


## How to install

### Install the code

This extension requires the GoCardlessPro PHP library. I have not packaged this up in this repo (need to find out best way to do this in CiviCRM) so here's how to install from the \*nix command line. You need [composer](https://getcomposer.org/download/)

    $ cd /path/to/your/extensions/dir
    $ git clone https://github.com/artfulrobot/uk.artfulrobot.civicrm.gocardless.git
    $ cd uk.artfulrobot.civicrm.gocardless
    $ which composer >/dev/null && composer install || echo You need composer, pls see https://getcomposer.org/download/

### Install the extension and create a payment processor

Install it through the CiviCRM Extensions screen as usual (you may need to click Refresh).

Go to Administer » CiviContribute » Payment Processors then click **Add New**

- Select **GoCardless** from the *Payment Processor Type*
- give it a name.
- Select **GoCardless Direct Debit** from the *Payment Method*
- Add your access tokens (you obvs need a GoCardless account to do this) and make up a secure webhook secret.
- click *Save*.

### Install your webhook at GoCardless

GoCardless has full separation of its test (sandbox) and live account management pages, so you'll do this twice. Be sure to supply the webhook secret appropriate to the test/live environments :-)

The webhook URL is at `/civicrm/gocardless/webhook` for Wordpress this would be
`?page=CiviCRM&q=civicrm/gocardless/webhook`

Note: the webhook will check the key twice; once against the test and once against the live payment processors' webhook secrets. From that information it determines whether it's a test or not.