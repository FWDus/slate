---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='https://www.fwd.us/api'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the FWD API! You can use our API to access FWD API endpoints.

We have language bindings in Shell! You can view code examples in the dark area to the right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:


```shell
# With shell, you can just pass the correct header with each request
curl "https://api.fwd.us/"
  -H "Authorization: examplekey"
```

> Make sure to replace `examplekey` with your API key.

FWD uses API keys to allow access to the API. You can register a new FWD API key at our [developer portal](https://www.fwd.us/api).

FWD expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: examplekey`

<aside class="notice">
You must replace <code>examplekey</code> with your personal API key.
</aside>

# Supporters

## Create a Supporter

```shell
curl -H "Authorization: examplekey" -H "Content-Type: application/json" -X POST -d '{"email":"supporter@email.com","postal_code":"94133"}' http://api.fwd.us/supporter
```

> Success Response:

```shell
{
  "status": 200,
  "data": {
    "vid": 3234574,
    "isNew": false
  }
}
```

> Multiple Districts Response:

```shell
{
  "status": 400,
  "message": "{{ postal_code }} belongs to more than one Congressional District. Please provide a full address."
}
```

This endpoint [creates or updates a Contact in HubSpot CRM](https://developers.hubspot.com/docs/methods/contacts/create_or_update). For the remainder of this document HubSpot Contacts will be referred to as Supporters.

Each request must either have a `postal_code` or a `full_address`.

### HTTP Request

`POST http://api.fwd.us/supporter`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
email | required | The email address is the primary key and unique identifier for a Supporter in HubSpot.
postal_code | optional | If a Postal Code is provided then the API needs to look up the Congressional District from [Google Civic API](https://developers.google.com/civic-information/). It should also look up the City, State/Region and Country via the [Google Geocoding API](https://developers.google.com/maps/documentation/geocoding/start?csw=1).<br /><br />If the result from [Google Civic API](https://developers.google.com/civic-information/) returns multiple Congressional Districts then the "Multiple District" error should be returned and the Supporter should not be saved in HubSpot.
full_address | optional | When a Full Address is provided via a [Google Place Autocomplete Address Form](https://developers.google.com/maps/documentation/javascript/examples/places-autocomplete-addressform) submission then Supporter's HubSpot properties should be populated with the Congressional District, Street Address, City, Postal Code, State/Region, Country.
hubspot_property | optional | A FWD signup form may include any [HubSpot Contact Property](https://app.hubspot.com/contacts/368496/settings/properties/).

<aside class="success">
Remember — a happy API endpoint is an authenticated API endpoint!
</aside>