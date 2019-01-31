---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

The Unmetric API is an easy way to query information about a brand's social media pages, accounts, metrics and related data. The API gives you the flexibility to feed Unmetric competitive intelligence into your in-house proprietary tools, native social media dashboards, command room screens and more.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# What Can You Do With The Unmetric REST API?
With the Unmetric API, you can:

* Gain a broad overview of a brand's social media activity 
* Trace fan and follower growth over time
* Delve deep into page and account social media performance by day
* Explore content published by the brand and related attributes
* Compare multiple brand profiles across metrics over time
* Get Daily Alerts on interesting brand social activity


# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Unmetric uses API keys to allow access to the API. You can request for a new unmetric API key from your account manager.

unmetric API expects for the API key to be included in all API requests to the server in a request parameter that looks like the following:

`{uri}?accesstoken=UNMETRICAPIKEY&additional_parameters`

<aside class="notice">
You must replace <code>UNMETRICAPIKEY</code> with your personal API key.
</aside>

# Brands

## Brand List

```shell
curl "http://api.unmetric.com/v2/api/brands?accesstoken=DA2B05835F41460392457B68757C2771&startdate=2015-08-01&enddate=2015-08-02&network=FB,TWT"
```

> The above command returns JSON structured like this:

```json
{
  "start_date": "2014-09-30",
  "end_date": "2014-12-02",
  "from_date": "2014-11-01",
  "to_date": "2014-12-02",
  "brands": {
    "FB": [
      {
        "id": "193619204022951",
        "name": "Rupeezone.in",
        "geography": "India",
        "industry": "Banking & Finance",
        "date_added": "2014-11-01",
        "url" : "https://www.facebook.com/RupeeZone"
      },
      {
        "id": "226936710654536",
        "name": "Imperial Optical Jamaica",
        "geography": "Jamaica",
        "industry": "Pharma & Health",
        "date_added": "2014-11-01",
        "url" : "https://www.facebook.com/Imperialopticaljamaica"
      }
    ],
    "TWT": [
      {
        "id": "ppdcro",
        "name": "PPD",
        "geography": "Worldwide",
        "industry": "Pharma & Health",
        "date_added": "2014-11-01",
        "url" : "https://twitter.com/ppdcro"
      },
      {
        "id": "covance",
        "name": "Covance",
        "geography": "Worldwide",
        "industry": "Pharma & Health",
        "date_added": "2014-11-01",
        "url" : "https://twitter.com/covance"
      }
    ]
  },
  "paging": {
    "prev": "https://api.unmetric.com/v2/api/brands?accesstoken=UNMETRICAPIKEY&startdate=2014-09-30&enddate=2014-12-02&fromdate=2014-10-01&todate=2014-10-31"
  }
}
```

This endpoint retrieves all brands added to unmetric's dashboard between the given time period.

### HTTP Request

`GET http://api.unmetric.com/v2/api/brands`

### Query Parameters

Parameter | Description
--------- | -----------
start_date | The date from which list of new brands are requested. 
end_date | The date till which data is requested.
network | A comma separated list of networks for which the list of brands is requested. The allowed values are FB, TWT, YT, PT, INS

<aside class="warning">
Note — start_date cannot be smaller than 2012-01-01 
</aside>

### Response Details

Field | Describtion
----- | -----------
id | This identifies the brand in its network and has one of the following values:  Facebook page id for ***Facebook*** network.  Twitter screen name for ***Twitter*** network. Instagram account name for ***Instagram*** network. Pinterest user name for ***Pinterest*** network. Youtube channel id for ***Youtube*** network.
name | The name of the Brand
url | The url of the profile for the network (eg Facebook page url for Facebook brand)
geography | The region of the Brand
industry | The industry of the Brand
date_added | The date the Brand was added to the Unmetric database
start_date | the start_date passed in request
end_date | The end_date passed in request
brands | The list brands for each network


## Search Brands

```shell
curl "http://api.unmetric.com/v2/api/brands/search?accesstoken=DA2B05835F41460392457B68757C2771&network=fb,twt&name=bmw"
```

> The above command returns JSON structured like this:

```json
{  
   "search_name":"bmw",
   "brands":{  
      "FB":[  
         {  
            "id":"309506851302",
            "name":"BMW USA",
            "geography":"United States",
            "industry":"Automotive",
            "date_added":"2012-01-01",
            "url":"https://www.facebook.com/BMWUSA/"
         },
         {  
            "id":"407584185042",
            "name":"BMW UK",
            "geography":"United Kingdom",
            "industry":"Automotive",
            "date_added":"2012-01-01",
            "url":"https://www.facebook.com/bmwuk/"
         }
      ],
      "TWT":[  
         {  
            "id":"BMWMotorsport",
            "name":"BMW Motorsport",
            "geography":"Germany",
            "industry":"Automotive",
            "date_added":"2012-01-12",
            "url":"https://twitter.com/BMWMotorsport"
         },
         {  
            "id":"bmwmotorradesp",
            "name":"BMW Motorrad Espa\u00F1a",
            "geography":"United States",
            "industry":"CUSTOM",
            "date_added":"2016-06-28",
            "url":"https://twitter.com/bmwmotorradesp"
         }
      ]
   }
}

```

This endpoint retrieves list of all brands with the given name.

### HTTP Request

`GET http://api.unmetric.com/v2/api/brands/search?accesstoken={accesstoken}&network={network}&name={brand_name}`

### URL Parameters

Parameter | Description
--------- | -----------
network | A comma separated list of networks for which the list of brands is requested. The allowed values are FB, TWT, YT, PT, INS
name | name of the brand

### Response Details

Field | Describtion
----- | -----------
id | This identifies the brand in its network and has one of the following values:  Facebook page id for ***Facebook*** network.  Twitter screen name for ***Twitter*** network. Instagram account name for ***Instagram*** network. Pinterest user name for ***Pinterest*** network. Youtube channel id for ***Youtube*** network.
name | The name of the Brand
url | The url of the profile for the network (eg Facebook page url for Facebook brand)
geography | The region of the Brand
industry | The industry of the Brand
date_added | The date the Brand was added to the Unmetric database
brands | The list brands for each network

## Dashboard brands list

```shell
curl "http://api.unmetric.com/v2/api/brands/dashboard?accesstoken=MYACCESSTOKEN&network=FB,TWT"
```

> The above command returns JSON structured like this:

```json
{
  "groups" : {
    "15369" : {
      "group_name" : "GROUP2-Bank",
      "brands" : {
        "FB" : [ {
          "id" : "7724542745",
          "name" : "Manchester United",
          "geography" : "United Kingdom",
          "industry" : "Sports",
          "data_available_from" : "2012-02-09",
          "url" : "https://www.facebook.com/manchesterunited/"
        }, {
          "id" : "230436000410837",
          "name" : "Ford Argentina",
          "geography" : "Argentina",
          "industry" : "Automotive",
          "data_available_from" : "2012-07-26",
          "url" : "https://www.facebook.com/fordargentina/"
        }, {
          "id" : "194737780569479",
          "name" : "Manchester United Arab Fans",
          "geography" : "Middle East",
          "industry" : "Sports",
          "data_available_from" : "2015-07-13",
          "url" : "https://www.facebook.com/arabic.manutd/"
        } ]
      }
    },
    "15368" : {
      "group_name" : "GROUP3-Food",
      "brands" : {
        "FB" : [ {
          "id" : "21785951839",
          "name" : "9GAG",
          "geography" : "Worldwide",
          "industry" : "Entertainment",
          "data_available_from" : "2012-01-01",
          "url" : "https://www.facebook.com/9gag/"
        } ]
      }
    },
    "15367" : {
      "group_name" : "GROUP1-Aviation",
      "brands" : {
        "TWT" : [ {
          "id" : "UHouston",
          "name" : "UniversityofHouston",
          "geography" : "United States",
          "industry" : "Education",
          "data_available_from" : "2015-07-06",
          "url" : "https://twitter.com/UHouston"
        } ]
      }
    }
  }
}
```

This endpoint returns all the groups with brands that the user created in unmetric analyze app.

### HTTP Request

`GET http://api.unmetric.com/v2/api/brands/dashboard?accesstoken={accesstoken}&network={network}`

### URL Parameters

Parameter | Description
--------- | -----------
network | A comma separated list of networks for which the list of brands is requested. The allowed values are FB, TWT, YT, PT, INS

### Response Details

Field | Describtion
----- | -----------
id | This identifies the brand in its network and has one of the following values:  Facebook page id for ***Facebook*** network.  Twitter screen name for ***Twitter*** network. Instagram account name for ***Instagram*** network. Pinterest user name for ***Pinterest*** network. Youtube channel id for ***Youtube*** network.
name | The name of the Brand
url | The url of the profile for the network (eg Facebook page url for Facebook brand)
geography | The region of the Brand
industry | The industry of the Brand
date_added | The date the Brand was added to the Unmetric database
group_name | Specifies the group name if the user saved that brand in a group. Group Id will be specified at the top of it
brands | The list brands for each network