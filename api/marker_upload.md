# Upload image

```
https://maphub.net/api/1/image/upload
```

This endpoint uploads a JPG or PNG image, resizes it to responsive sizes and stores it on the server.

For this endpoint you'll need to

- send the arguments as a JSON encoded string in the `MapHub-API-Arg` header
- send the uploaded file as binary data in the request body


## Arguments

- **file_type** (required): one of `jpg`, `png`

## Response

- **image_id**: the id of the image
- **width**: the width of the image in pixels
- **height**: the height of the image in pixels
- **tip_color**: the color of the image popup's tip at the bottom center
- **avg_color**: the average color of the image, displayed before loading
- **has_gps**: if the image has GPS information, true/false
- **geometry**: GeoJSON geometry if the image has GPS information. null if not.
- **date_str**: image's original created date in a human readable text
- **date_iso**: image's original created date in ISO datetime format

## Limitations

Following limits apply to uploads:

- maximum file size 15 MB
- maximum processing time 2 minutes

On a MapHub Enterprise server, there are no limits. If you are interested in MapHub Enterprise, [contact&nbsp;us](https://maphub.net/contact/sales).

## Code example

### curl

```
curl https://maphub.net/api/1/image/upload \
    --header 'Authorization: Token <api_key>' \
    --header 'MapHub-API-Arg: {"file_type": "png"}' \
    --data-binary @test.png
```

### Python

```python
import json
import requests

url = 'https://maphub.net/api/1/image/upload'

api_key = '<api_key>'

args = {
    'file_type': 'jpg',
}

headers = {
    'Authorization': 'Token ' + api_key,
    'MapHub-API-Arg': json.dumps(args),
}

with open('test.jpg', 'rb') as f:
    r = requests.post(url, headers=headers, data=f)

print(r.json())
```

