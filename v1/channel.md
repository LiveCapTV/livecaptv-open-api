# Channel

| Endpoint | Description |
| ---- | --------------- |
| [POST /channel/ping](/v1/channel.md#ping) | Prepare server for capturing a stream |
| [POST /channel/capture](/v1/channel.md#capture) | Take capture of a live stream |

## `POST /channel/ping`

Notify server of getting prepared for taking a capture. If there are no PING requests for a live stream in 5 minutes, capturing resources for this live stream may get recycled.

### Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th width="50">Type</th>
            <th width=100%>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>platform</code></td>
            <td>required</td>
            <td>string</td>
            <td>Name of live stream platform. Choices: <code>twitch</code></td>
        </tr>
        <tr>
            <td><code>channel</code></td>
            <td>required</td>
            <td>string</td>
            <td>Name of live stream channel. For Twitch channels, this string would be the same as in <code>https://twitch.tv/***</code></td>
        </tr>
    </tbody>
</table>

### Response Handling

Possible server response values include:

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th width="50">Type</th>
            <th width=100%>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>status</code></td>
            <td>string</td>
            <td>Status of capture service. Choices: <code>ok, not_available</code></td>
        </tr>
        <tr>
            <td><code>nextPing</code></td>
            <td>number</td>
            <td>Number of seconds that is suggested for the client to wait before sending another ping request.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -XPOST -i -H 'Accept: application/json'\
-H 'LiveCap-Access-Token: AoBXBCqC4wVFgMHUaUeY86oPnUMrMnM4u'\
-d "platform=twitch&channel=riotgames" \
'https://api.livecap.tv/v1/channel/ping' 
```

### Example Response

```json
{
	"status": "ok",
    "nextPing": 5
}
```

## `POST /channel/capture`

Take capture of a live stream

### Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th width="50">Type</th>
            <th width=100%>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>platform</code></td>
            <td>required</td>
            <td>string</td>
            <td>Name of live stream platform. Choices: <code>twitch</code></td>
        </tr>
        <tr>
            <td><code>channel</code></td>
            <td>required</td>
            <td>string</td>
            <td>Name of live stream channel. For Twitch channels, this string would be the same as in <code>https://twitch.tv/***</code></td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -XPOST -i -H 'Accept: application/json'\
-H 'LiveCap-Access-Token: AoBXBCqC4wVFgMHUaUeY86oPnUMrMnM4u'\
-d "platform=twitch&channel=riotgames" \
'https://api.livecap.tv/v1/channel/capture' 
```

### Example Response (Request succeeded)

```json
{
	"status": "ok",
    "capture": {
        "id": "uLMjA0PqyDe",
        "shareURL": "https://www.livecap.tv/t/riotgames/uLMjA0PqyDe"
    }
}
```

### Example Response (Request failed)

```json
{
    "status": "error",
    "message": "Server does not feel like taking a capture today."
}
```
