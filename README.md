# LiveCapTV API v1

## Overview

The LiveCapTV API enables you to develop your own applications using the rich feature set that we provide. Features include retrieving data about our captures and taking a capture of a live stream. The following pages list the resources that the LiveCapTV API provides. If you have any questions or need help in using this API, please contact us at [api-support@livecap.tv][]. Bugs can be reported on our [Github Issues][].

[api-support@livecap.tv]: mailto:api-support@livecap.tv
[Github Issues]: https://github.com/LiveCapTV/livecaptv-open-api/issues

## API Endpoint

https://api.livecap.tv/v1/ (Still under development. Not published yet)

## API Index

### [Captures](/v1/api/capture.md)

| Endpoint | Description |
| ---- | --------------- |
| [GET /captures](/v1/api/capture.md#list-captures) | Get list of captures |

### [Channels](/v1/api/channel.md)

| Endpoint | Description |
| ---- | --------------- |
| [POST /channel/ping](/v1/api/channel.md#ping) | Prepare server for capturing a stream |
| [POST /channel/capture](/v1/api/channel.md#capture) | Take capture of a live stream |



