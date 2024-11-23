# ESPHome project for smart home box

## Wi-Fi creds
- `esp_smart_home` / `rubberduck_soup_#^24`
- livingroom: `comfybed2024`

## Compile and upload
```bash
# for first flashing, add: --device=/dev/ttyUSB0
docker run --rm -v "./esphome":/config -it ghcr.io/esphome/esphome:2024.11.1 run smarthome.yaml
```
