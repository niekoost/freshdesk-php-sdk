# Freshdesk PHP SDK API v2 

[![Build Status](https://travis-ci.org/mpclarkson/freshdesk-php-sdk.svg?branch=master)](https://travis-ci.org/mpclarkson/freshdesk-php-sdk)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/mpclarkson/freshdesk-php-sdk/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/mpclarkson/freshdesk-php-sdk/?branch=master)

This is a PHP SDK for the [Freshdesk](https://www.freshdesk.com) API v2.

If you have questions, please contact me or open issue on GitHub.

## Quick Start
```php
require __DIR__ . '/vendor/autoload.php';
use \Freshdesk\Api;

$api = new Api("your_freshdesk_api_key", "your_freshdesk_domain");

$all = $api->tickets->all(); //List tickets (page 1)
$some = $api->tickets->all(['page' => 2]); //List all tickets (page 2)
$new = $api->tickets->create($data); //Create a new ticket
$updated = $api->tickets->update($data); //Update a ticket
$api->tickets->delete($id); //Delete a ticket
$existing = $api->tickets->view($id); //View a ticket

//Responses are simple arrays, e.g.:
$id = $existing['id'];
$first = $all[0];

```

## Installation
To integrate this library into your application, use [Composer](https://getcomposer.org).

Add `mpclarkson/freshdesk-php-sdk` to your **composer.json** file:

```json
{
    "require": {
        "mpclarkson/freshdesk-php-sdk": "dev-master"
    }
}

```

Then run:

```bash
php composer.phar install
```

## API Overview

Full documentation is coming soon.

### Getting started

Creating a new API instance is very easy. All you need is your Freshdesk 
API key and your Freshdesk domain.

```php
require __DIR__ . '/vendor/autoload.php';
use \Freshdesk\Api;

$api = new Api("your_freshdesk_api_key", "your_freshdesk_domain");
```

### Resources

The available methods for each resource are available via a public
property on the api, for example:

```php
//Contacts
$contacts = $api->contacts->update($contactId, $data);

//Agents
$me = $api->agents->current();

//Companies
$company = $api->companies->create($data);

//Groups
$deleted = $api->groups->delete($groupId);

//Tickets
$ticket = $api->tickets->view($filters);

//Time Entries
$time = $api->timeEntries->all($ticket['id]);

//Categories
$newCategory = $api->categories->create($data);

//Forums
$forum = $api->forums->create($categoryId, $data);

//Topics
$topics - $api->topics->monitor($topicId, $userId);

//Comments
$comment = $api->comments->create($forumId);

//Email Configs
$configs = $api->emailConfigs->all();

//Products
$product = $api->products->view($productId);

//Business Hours
$hours = $api->businessHours->all();

//SLA Policy
$policies= $api->slaPolicies-all();

```

### Responses

All responses are arrays of data. Please refer to Freshdesk's documentation
for further information. 


### Filtering

All `GET` requests accept an optional `array $query` parameter to filter
results. For example:

```php

//Page 2 with 50 results per page
$page2 = $this->forums->all(['page' => 2, 'per_page' => 50]);

//Tickets for a specific customer
$tickets = $this->tickets->view(['company' => $companyId]);

```

Please read the Freshdesk documentation for further information on
filtering `GET` requests.


## To Do

This is a work in progress and PRs are welcome.

So far all api calls are available except for the `Solutions` and `Surveys`, 
which Freshdesk has not yet implemented.

- [] Solutions
- [] Surveys
- [] More tests. You can never have enough!

## Author

The library was written and maintained by [Matthew Clarkson](http://mpclarkson.github.io/) 
from [Hilenium](https://hilenium.com).


## Reference

* [Freshdesk API Documentation](https://developer.freshdesk.com/api/)
