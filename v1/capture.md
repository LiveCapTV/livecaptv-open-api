# Captures

| Endpoint | Description |
| ---- | --------------- |
| [GET /captures](/v1/api/capture.md#list-captures) | Get list of captures |

## `GET /captures`

Returns a list of Capture object

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

