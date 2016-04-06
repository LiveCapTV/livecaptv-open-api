# LiveCapTV API v1

## Overview

The LiveCapTV API enables you to develop your own applications using the rich feature set that we provide. Features include retrieving data about our hottest captures and taking a capture of a live stream. The following pages list the resources that the LiveCapTV API provides. If you have any questions or need help in using this API, please contact us at [api-support@livecap.tv][]. Bugs can be reported on our [Github Issues][].

[api-support@livecap.tv]: mailto:api-support@livecap.tv
[Github Issues]: https://github.com/LiveCapTV/livecaptv-open-api/issues

## API Endpoint

https://api.livecap.tv/v1/ (Still under development. Not published yet.)

## Authentication

Before using our API, you must [register an application][] and generate your API token in our system. This token should be sent as HTTP Request header or in query string.

### Example - Sending AccessToken as HTTP Request header

```
curl -i -H 'Accept: application/json'\
-H 'LiveCap-Access-Token: AoBXBCqC4wVFgMHUaUeY86oPnUMrMnM4u'\
'https://api.livecap.tv/v1/video' 
```

### Example - Sending AccessToken in query string

```
curl -i -H 'Accept: application/json'\
'https://api.livecap.tv/v1/video?token=AoBXBCqC4wVFgMHUaUeY86oPnUMrMnM4u' 
```

Note that all requests to our endpoints should be sent via HTTPS to avoid token leaks.

[register an application]: /v1/trial.md#register

## API Index

### [Query Videos Data](/v1/video.md)

| Endpoint | Description |
| ---- | --------------- |
| [GET /v1/video/list](/v1/video.md#list-videos) | Get list of videos |
| [GET /v1/video/:videoID](/v1/video.md#get-video) | Get details of a video |

### [Cap Live Streams](/v1/stream.md)

| Endpoint | Description |
| ---- | --------------- |
| [POST /v1/stream/ping](/v1/stream.md#ping) | Prepare server for capping a live stream |
| [POST /v1/stream/cap](/v1/stream.md#cap) | Cap of a live stream |

## Limitations

To avoid abusing our API, rates of requests are limited on a daily basis.
