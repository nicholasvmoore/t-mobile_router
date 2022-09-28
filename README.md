T-Mobile 5G Router
---
This guide will help you disable the Wi-Fi on the Arcadyan KVD21 Gateway

## Obtain auth token and set to Enviroment Variable
```bash
curl -X POST http://192.168.12.1/TMI/v1/auth/login -d '{"username": "admin", "password": "$whateverYourPasswordIs" }'
```

## Login and grab current config
```bash
curl http://192.168.12.1//TMI/v1/network/configuration\?get\=ap -H 'Authorization: Bearer $environmentVariable' > ~/Desktop/t-mobile-wifi-info.txt
```

## Disable the 2.4ghz and 5.8ghz radios
```bash
# isRadioEnabled set to False

{"2.4ghz":{"isRadioEnabled":false,"mode":"auto","airtimeFairness":true,"channelBandwidth":"Auto","channel":"Auto","transmissionPower":"100%","isWMMEnabled":true,"isMUMIMOEnabled":true,"maxClients":128,"ssid":{"ssidName":"TMOBILE-DE61","wpaKey":"rambling.motion.stipulate.public","steered":true,"isBroadcastEnabled":true,"encryptionVersion":"WPA2/WPA3","encryptionMode":"AES"},"ssidGuest":{"ssidName":"TMOBILE-guest-DE60","wpaKey":"123456789","steered":true,"isBroadcastEnabled":true,"encryptionVersion":"WPA2/WPA3","encryptionMode":"AES"}},"5.0ghz":{"isRadioEnabled":false,"mode":"auto","airtimeFairness":true,"channelBandwidth":"Auto","channel":"Auto","transmissionPower":"100%","isWMMEnabled":true,"isMUMIMOEnabled":true,"maxClients":128,"ssid":{"ssidName":"TMOBILE-DE61","wpaKey":"rambling.motion.stipulate.public","steered":true,"isBroadcastEnabled":true,"encryptionVersion":"WPA2/WPA3","encryptionMode":"AES"},"ssidGuest":{"ssidName":"TMOBILE-guest-DE60","wpaKey":"123456789","steered":true,"isBroadcastEnabled":true,"encryptionVersion":"WPA2/WPA3","encryptionMode":"AES"}}}

cat ~/Desktop/t-mobile-wifi-info.txt | curl -d "@-" http://192.168.12.1/TMI/v1/network/configuration\?set\=ap -H 'Authorization: Bearer $environmentVariable'
```
