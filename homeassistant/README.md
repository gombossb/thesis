```bash
docker compose up [-d]
```

## Wi-Fi creds
- `esp_smart_home` / `rubberduck_soup_#^24`
- livingroom: `comfybed2024`

## Compile and upload
```
docker run --rm -v "./esphome_config":/config -it ghcr.io/esphome/esphome:2024.9.0 run livingroom.yaml
```
