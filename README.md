# LiveCapTV API v1

## Overview

The LiveCapTV API enables you to develop your own applications using the rich feature set that we provide. Features include retrieving data about our hottest captures and taking a capture of a live stream. The following pages list the resources that the LiveCapTV API provides. If you have any questions or need help in using this API, please contact us at [api-support@livecap.tv][]. Bugs can be reported on our [Github Issues][].

[api-support@livecap.tv]: mailto:api-support@livecap.tv
[Github Issues]: https://github.com/LiveCapTV/livecaptv-open-api/issues

## API Endpoint

https://api.livecap.tv/

## Authentication

Before using our API, you must [register an application][] and generate your API token in our system. This token should be sent as HTTP Request header or in query string together with the application ID.

### Example - Sending ApplicationID and AccessToken as HTTP Request header

```
curl -i -H 'Accept: application/json' -H 'LiveCap-App-Key: be85d651-95f3-4d2d-b587-2e86b39ab142' -H 'LiveCap-Access-Token: c77ca215-8a83-4888-afe4-06d53034e4c8' -H 'Origin: https://foo.bar' -XGET 'https://api.livecap.tv/v1/video/list'
```

### Example - Sending ApplicationID and AccessToken in query string

```
curl -i -H 'Accept: application/json' -H 'Origin: https://foo.bar' -XGET 'https://api.livecap.tv/v1/video/list?appid=be85d651-95f3-4d2d-b587-2e86b39ab142&token=c77ca215-8a83-4888-afe4-06d53034e4c8'
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
| [POST /v1/stream/cap](/v1/stream.md#cap) | Take capture of a live stream |

### [Cap VODs](/v1/vod.md)

| Endpoint | Description |
| ---- | --------------- |
| [POST /v1/vod/cap](/v1/vod.md#cap) | Take capture of a VOD |

## Other Utilities

[LiveCapTV Embedded Player](/v1/player.md)

## Limitations

To avoid abusing our API, rates of requests are limited on a daily basis.
