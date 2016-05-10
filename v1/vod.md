# Capping VODs

| Endpoint | Description |
| ---- | --------------- |
| [POST /v1/vod/cap](/v1/vod.md#cap) | Take capture of a VOD |

Recommended workflow for capping a VOD:

- Send CAP request to API endpoint and get video in the server response
- After capping, keep polling video metadata until video status becomes "published"
- Tell your user the "shareURL" of the video 

## `POST /v1/vod/cap`

Cap a VOD

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
            <td>Name of VOD platform. Choices: <code>twitch</code></td>
        </tr>
        <tr>
            <td><code>vod</code></td>
            <td>required</td>
            <td>string</td>
            <td>ID of the VOD. For Twitch VODs, this string would be the <code>vod_id</code> as in <code>https://www.twitch.tv/{channel)name}/v/{vod_id}</code></td>
        </tr>
        <tr>
            <td><code>start</code></td>
            <td>required</td>
            <td>number</td>
            <td>Time of start in milliseconds.</td>
        </tr>
        <tr>
            <td><code>length</code></td>
            <td>optional</td>
            <td>number</td>
            <td>Time of capping duration in milliseconds. Defaults to 60000(one minute).</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -i -XPOST  -H 'Accept: application/json' -H 'LiveCap-App-Key: be85d651-95f3-4d2d-b587-2e86b39ab142' -H 'LiveCap-Access-Token: c77ca215-8a83-4888-afe4-06d53034e4c8' -H 'Origin: https://foo.bar' -H 'Content-Type: application/x-www-form-urlencoded' -d 'platform=twitch&vod=59592371&start=0&length=60000' 'https://api.livecap.tv/v1/vod/cap'
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
          "avatarURL":"http://dxm2idf2u6bml.cloudfront.net/public/images/profile.jpg",
          "twitchAccountName":"tlyee"
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
