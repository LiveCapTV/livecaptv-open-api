# Captures

| Endpoint | Description |
| ---- | --------------- |
| [GET /captures](/v1/capture.md#list-captures) | Get list of captures |

## `GET /captures`

Returns a list of Capture object

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
            <td>Name of live stream platform. Should be used together with `channel` parameter. Choices: <code>twitch</code></td>
        </tr>
        <tr>
            <td><code>channel</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Name of live stream channel. Should be used together with `platform` parameter. For Twitch channels, this string would be the same as in <code>https://twitch.tv/***</code></td>
        </tr>
        <tr>
            <td><code>ts_start</code></td>
            <td>optional</td>
            <td>number</td>
            <td>Timestamp in milliseconds. When this param is included in the request, only captures taken **after** this timestamp will be included in the result.</td>
        </tr>
        <tr>
            <td><code>ts_end</code></td>
            <td>optional</td>
            <td>number</td>
            <td>Timestamp in milliseconds. When this param is included in the request, only captures taken **before** this timestamp will be included in the result.</td>
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
            <td><code>views_min</code></td>
            <td>optional</td>
            <td>number</td>
            <td>Minimum number of views needed for a capture to be included in the result. Defaults to 0.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/json' \
-X GET https://api.livecap.tv/captures
```

### Example Response

```json
{
	"captures": [
		{
			"id": "TBD"
		}
	]	
}
```

