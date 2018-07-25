---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Saturnus is a Webhook-as-a-Service. You can schedule webhooks and also make them recurring.
Once a webhook is configured, it will try POSTing to the specified URL as many times as configured in the *retries* parameter. Only HTTP Status 200 is considered a success. Requests should answer in less than 10 seconds.


# Create a Hook

## HTTP Request

```shell
curl https://api.saturnus.io/v1/hook \
-H `Content-Type: application/json` \
-d `{
        "key": "MY_KEY",
        "url": "https://endpoint.com/my_path",
        "when": "2018-07-30T05:00:00Z",
        "every": "2 hours",
        "retries": 3,
        "data": {
          "foo": "bar"
        },
        "content_type": "application/json"
    }`
```

> Response (HTTP Status 200)

```json
"Hook ID"
```

## Query Parameters

Name | Required | Type | Default | Description
---- | -------- | ---- | ------- | -----------
key | yes | string | | The API key
url | yes | string | | The POST endpoint
when | yes | string | | A ISO8601 date for when to fire the webhook
every | no | string | "disabled" | A human readable interval. Example: "3 days and 4 hours"
retries | no | number | 2 | The number of retries. Maximum 5.
data | no | object | | A object containing parameters to send to the endpoint.
content_type | no | string | "application/json" | The content type of the endpoint. Example: "application/x-www-form-urlencoded"

# List Hooks

<aside class="notice">
This API displays 100 hooks per page.
</aside>

```shell
curl --request GET https://api.saturnus.io/v1/hooks \
-H `Content-Type: application/json` \
-d `{
        "key":"MY_KEY",
        "interval": ["2018-07-01T00:00:00Z","2018-07-30T23:59:59Z"],
        "filter": [{
          "comparator": "eq",
          "field": "status",
          "value": "pending"
        }]
    }`
```

> Response

```json
{ "data": [....], "next": "PAGINATION_URL" }
```

## Query Parameters

Name | Required | Type | Default | Description
---- | -------- | ---- | ------- | -----------
key | yes | string | | The API key
interval | yes | array | | An array of ISO8601 dates containing the interval to get hooks by creation date
filter | no | array | | A array of conditions to filter the hooks to be listed


# Get a Hook Information

```shell
curl --request GET https://api.saturnus.io/v1/hook/ID
```

> Response

```json
{
  "id": "Hook id",
  "created_at": "ISO8601 date",
  "updated_at": "ISO8601 date of when it fired",
  "url": "Endpoint URL",
  "retries": "Number of retries",
  "data": "Object containing data to be sent to the endpoint",
  "when": "ISO8601 date",
  "status": "Can be completed, pending or error",
  "error": "An object containing the HTTP Status and the endpoint response if the status is 'error'",
  "content_type": "Endpoint content type"
}
```

# Delete a Hook

```shell
curl --request DELETE https://api.saturnus.io/v1/hook/ID
```

> Response

```json
"OK"
```