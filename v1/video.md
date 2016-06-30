# Video

| Endpoint | Description |
| ---- | --------------- |
| [GET /v1/video/list](/v1/video.md#list-videos) | Get list of videos |
| [GET /v1/video/:videoID](/v1/video.md#get-video) | Get details of a video |

## `GET /v1/video/list`

Returns a list of Video objects

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
            <td>optional</td>
            <td>string</td>
            <td>Name of live stream platform. Should be used together with <code>channel</code> parameter. Choices: <code>twitch</code></td>
        </tr>
        <tr>
            <td><code>channel</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Name of live stream channel. If this field is given, only videos that belong to the given channel will be included in the result. Should be used together with <code>platform</code> parameter. For Twitch channels, this string would be the same as in <code>https://twitch.tv/***</code></td>
        </tr>
        <tr>
            <td><code>game</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Name of game. If this field is given, only videos of the given game will be included in the result. Examples are <code>League of Legends</code>, <code>Dota 2</code></td>
        </tr>
        <tr>
            <td><code>ts_start</code></td>
            <td>optional</td>
            <td>number</td>
            <td>Timestamp in milliseconds. When this param is included in the request, only videos taken <b>after</b> this timestamp will be included in the result.</td>
        </tr>
        <tr>
            <td><code>ts_end</code></td>
            <td>optional</td>
            <td>number</td>
            <td>Timestamp in milliseconds. When this param is included in the request, only videos taken <b>before</b> this timestamp will be included in the result.</td>
        </tr>
        <tr>
            <td><code>limit</code></td>
            <td>optional</td>
            <td>number</td>
            <td>Maximum number of results included in the result. Typically used in pagination. This number defaults to 20 and can be 100 maximum.</td>
        </tr>
        <tr>
            <td><code>offset</code></td>
            <td>optional</td>
            <td>number</td>
            <td>Number of records skipped in the result list. Defaults to 0. Typically used in pagination.</td>
        </tr>
        <tr>
            <td><code>sort</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Sorting rules. Options: <code>top</code>(order by num_views desc), <code>latest</code>(order by capping time desc). Defaults to <code>latest</code></td>
        </tr>
        <tr>
            <td><code>views_min</code></td>
            <td>optional</td>
            <td>number</td>
            <td>Minimum number of views needed for a video to be included in the result. Defaults to 0.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/json' -H 'LiveCap-App-Key: be85d651-95f3-4d2d-b587-2e86b39ab142' -H 'LiveCap-Access-Token: c77ca215-8a83-4888-afe4-06d53034e4c8' -XGET 'https://api.livecap.tv/v1/video?platform=twitch&channel=riotgames'
```

### Example Response

```json
[
    {  
        "id":"uLMjA0PqyDe",
        "title":"LCK Spring - Week 1 Day 4",
        "status": "published",
        "created":1452934202922,
        "views":54689,
        "upvotes":2,
        "shareURL":"http://www.livecap.tv/t/riotgames/uLMjA0PqyDe",
        "author":{  
          "name":"tlyee",
          "displayName":"tlyee",
          "avatarURL":"http://dxm2idf2u6bml.cloudfront.net/public/images/profile.jpg",
          "twitchAccountName":"tlyee"
        },
        "video": {
            "high": "http://d1qugqs02rnrk6.cloudfront.net/f1fad403-f7f0-4cee-83a5-80f2a6446c84.mp4",
            "medium": "http://d1qugqs02rnrk6.cloudfront.net/ff14ec4c-8b67-47ee-b4a6-9849646372e2.mp4",
            "low": "http://d1qugqs02rnrk6.cloudfront.net/e693c337-b3f5-4eb7-876d-751e993484ed.mp4"
        },
        "preview": {
            "URL": "http://dxm2idf2u6bml.cloudfront.net/rest/serve/THUMBNAILS/d1256087-5f36-4278-91b0-fc2814d54648.jpg",
            "thumbnailURL": "http://dxm2idf2u6bml.cloudfront.net/rest/serve/THUMBNAILS/d1256087-5f36-4278-91b0-fc2814d54648.jpg?width=350",
            "color": "#bcb29e",
        },
        "channel": {
            "platform": "twitch",
            "name": "riotgames"
        },
        "game": {
            "name": "League of Legends"
        }
    }
]   
```

## `GET /v1/video/:videoID`

Get details of a Video object

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
            <td><code>videoID</code></td>
            <td>required</td>
            <td>string</td>
            <td>ID if the Video object</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/json' -H 'LiveCap-App-Key: be85d651-95f3-4d2d-b587-2e86b39ab142' -H 'LiveCap-Access-Token: c77ca215-8a83-4888-afe4-06d53034e4c8' -XGET 'https://api.livecap.tv/v1/video/uLMjA0PqyDe'
```

### Example Response

```json
{  
    "id":"uLMjA0PqyDe",
    "title":"LCK Spring - Week 1 Day 4",
    "status": "published",
    "created":1452934202922,
    "views":54689,
    "upvotes":2,
    "shareURL":"http://www.livecap.tv/t/riotgames/uLMjA0PqyDe",
    "author":{  
      "name":"tlyee",
      "displayName":"tlyee",
      "avatarURL":"http://dxm2idf2u6bml.cloudfront.net/public/images/profile.jpg",
      "twitchAccountName":"tlyee"
    },
    "video": {
        "high": "http://d1qugqs02rnrk6.cloudfront.net/f1fad403-f7f0-4cee-83a5-80f2a6446c84.mp4",
        "medium": "http://d1qugqs02rnrk6.cloudfront.net/ff14ec4c-8b67-47ee-b4a6-9849646372e2.mp4",
        "low": "http://d1qugqs02rnrk6.cloudfront.net/e693c337-b3f5-4eb7-876d-751e993484ed.mp4"
    },
    "preview": {
        "URL": "http://dxm2idf2u6bml.cloudfront.net/rest/serve/THUMBNAILS/d1256087-5f36-4278-91b0-fc2814d54648.jpg",
        "thumbnailURL": "http://dxm2idf2u6bml.cloudfront.net/rest/serve/THUMBNAILS/d1256087-5f36-4278-91b0-fc2814d54648.jpg?width=350",
        "color": "#bcb29e",
    },
    "channel": {
        "platform": "twitch",
        "name": "riotgames"
    },
    "game": {
        "name": "League of Legends"
    }
}   
```

