# Capping Live Streams

| Endpoint | Description |
| ---- | --------------- |
| [POST /v1/stream/ping](/v1/stream.md#ping) | Prepare server for capping of a live stream |
| [POST /v1/stream/cap](/v1/stream.md#cap) | Cap a live stream |

Recommended workflow for capping a live stream:

- Keep sending PING requests when watching a live stream channel
- Send CAP requests only when "status" in PING response is "ok"
- After capping, keep polling video metadata until video status becomes "published"
- Tell your user the "shareURL" of the video 

## `POST /v1/stream/ping`

Notify server of getting prepared for capping. If there are no PING requests for a live stream in 5 minutes, capturing resources for this live stream may get recycled.

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
            <td>Status of capture service. Choices: <code>ok</code>, <code>not_available</code><a href="/v1/faq.md" target="_self">(Why?)</a></td>
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
curl -i -XPOST  -H 'Accept: application/json' -H 'LiveCap-App-Key: be85d651-95f3-4d2d-b587-2e86b39ab142' -H 'LiveCap-Access-Token: c77ca215-8a83-4888-afe4-06d53034e4c8' -H 'Origin: https://foo.bar' -H 'Content-Type: application/x-www-form-urlencoded' -d 'platform=twitch&channel=riotgames' 'https://api.livecap.tv/v1/stream/ping'
```

### Example Response

```json
{
	"status": "ok",
    "nextPing": 5
}
```

## `POST /v1/stream/cap`

Cap a live stream

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
        <tr>
            <td><code>offset</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Number of seconds the captured moment differs from where the live stream is now at. If this parameter is set to <code>none</code>, then the latest <b>60</b> seconds of live stream are captured. For almost all times this value is <b>negative</b> because it takes time for the client to download and play the latest video segment. If you would like to inject your code on Twitch playback page, you could refer to <a href="/v1/twitch_player_offset.md" target="_self">this document</a> for telling how much the client is falling behind the up-to-date live stream. Default: <code>none</code></td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -i -XPOST  -H 'Accept: application/json' -H 'LiveCap-App-Key: be85d651-95f3-4d2d-b587-2e86b39ab142' -H 'LiveCap-Access-Token: c77ca215-8a83-4888-afe4-06d53034e4c8' -H 'Origin: https://foo.bar' -H 'Content-Type: application/x-www-form-urlencoded' -d 'platform=twitch&channel=riotgames&offset=-15' 'https://api.livecap.tv/v1/stream/cap'
```

### Example Response (Request succeeded)

```json
{
	"status": "ok",
    "video": {  
        "id":"uLMjA0PqyDe",
        "title":"LCK Spring - Week 1 Day 4",
        "status": "draft",
        "created":1452934202922,
        "views":0,
        "upvotes":0,
        "shareURL":"http://www.livecap.tv/t/riotgames/uLMjA0PqyDe",
        "author":{  
          "name":"tlyee",
          "displayName":"tlyee",
          "avatarURL":"http://dxm2idf2u6bml.cloudfront.net/public/images/profile.jpg"
        },
        "video": {

        },
        "preview": {
            
        },
        "channel": {
            "platform": "twitch",
            "name": "riotgames"
        },
        "game": {
            "name": "League of Legends"
        }
    }
}
```

### Example Response (Request failed)

```json
{
    "status": "error",
    "message": "Server does not feel like taking a cap today."
}
```
