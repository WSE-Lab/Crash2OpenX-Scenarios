# Video gallery

| File | Contents |
| --- | --- |
| [index.html](index.html) | Collection gallery with links to all ten scenarios, maps, videos, source reports, and measurements. |
| [showcase.mp4](showcase.mp4) | Combined showcase video. |

From the repository root, run:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Open **http://localhost:8000/preview/** in a browser. No CARLA installation is required. Stop the server with Ctrl+C.

Individual interaction clips and road images live in each scenario's `preview/` directory. Full recorded RGB videos live in its `evidence/` directory. The gallery keeps the original Chinese descriptions; use the [English scenario catalog](../scenarios/README.md) to read the interactions and outcomes.
