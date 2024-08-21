# 🎸 Riffusion API

This repo contains instructions for using the Riffusion API to create music
based on sound prompts and lyrics.

## Usage

Add your API key:

```bash
export RIFFUSION_API_KEY=<your-api-key>
```

Run via Python:

```python
import base64
import os
import requests

response = requests.post(
    'https://backend.riffusion.com/v1/riff',
    headers={
        'Content-Type': 'application/json',
        'Api-Key': os.environ.get("RIFFUSION_API_KEY"),
    },
    json={
        'prompts': [
            { "text": "chillstep pop" },
        ],
        'lyrics': "Hello from outer space\nCan you hear me?",
    },
).json()

with open("output.wav", "wb") as f:
    f.write(base64.b64decode(response["audio_b64"]))
```

Run via Python with strong types:

```python
from riffusion.api import generate_music, Prompt, RiffRequest

response = generate_music(
    RiffRequest(
        prompts=[
            Prompt(text="chillstep pop"),
        ],
        lyrics="Hello from outer space\nCan you hear me?",
    )
)

import base64
with open("output.wav", "wb") as f:
    f.write(base64.b64decode(response.audio_b64))
```

Run via curl:

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Api-Key: ${RIFFUSION_API_KEY}" \
  -d '{"prompts": [{"text": "chillstep pop"}], "lyrics": "Hello from outer space\nCan you hear me?"}' \
  https://backend.riffusion.com/v1/riff \
  | jq -r .audio_b64 | base64 -d > output.wav
```

## Examples

TODO

## Streamlit Demo

Run:

```bash
python -m streamlit run demo_app.py
```

Hosted at:

TODO
