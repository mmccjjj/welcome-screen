api key: AIzaSyBnkrLzmcWjKBf7TdGATCrf6SmpfKW_Kjw
sheetId: 1hzQjE8BH0Ilm8nam7sNRKRyAsd9akxQdKjLz4oBF8is

https://sheets.googleapis.com/v4/spreadsheets/1hzQjE8BH0Ilm8nam7sNRKRyAsd9akxQdKjLz4oBF8is/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=AIzaSyBnkrLzmcWjKBf7TdGATCrf6SmpfKW_Kjw



---

MeteoApi


ConsumerKey: 
uEX4iBjXrXwTgEu8FkisjiF83eiunD81

ConsumerSecret:https://api.srgssr.ch/srf-meteo/geolocationNames?zip=8045
VBdOcHvT0EEZORWg

encode: 

echo -n ConsumerKey:ConsumerSecret | base64

encoded Key&Secret

dUVYNGlCalhyWHdUZ0V1OEZraXNqaUY4M2VpdW5EODE6VkJkT2NIdlQwRUVaT1JXZw

cUrlRequest: (get Token)

curl -X POST \
  'https://api.srgssr.ch/oauth/v1/accesstoken?grant_type=client_credentials' \
  -H 'Authorization: Basic <Encoded Consumer Key & Consumer Secret>' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Length: 0' \
  -H 'Postman-Token: [token]'

accessToken: (valid 7 days)

3ulADlktGGVwNiK1yblJ5ElAUU1o

cUrlRequest: (use Token)

curl -X GET \
  'http://api.srgssr.ch/rts/archives/v2/audios' \
  -H 'Authorization: Bearer <access_token>' \
  -H 'Cache-Control: no-cache' \
  -H 'Postman-Token: [token]'

  curl -X GET \
  'https://api.srgssr.ch/srf-meteo/geolocationNames?zip=8045' \
  -H 'Authorization: Bearer 3ulADlktGGVwNiK1yblJ5ElAUU1o' \
  -H 'Cache-Control: no-cache' 
 



curl -X POST \
  'https://api.srgssr.ch/oauth/v1/accesstoken?grant_type=client_credentials' \
  -H 'Authorization: Basic base64<dUVYNGlCalhyWHdUZ0V1OEZraXNqaUY4M2VpdW5EODE6VkJkT2NIdlQwRUVaT1JXZw>' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Length: 0' \
  -H 'Postman-Token: XX264e32-2de0-f1e3-f3f8-eab014bbXX76'


  https://api.srgssr.ch/srf-meteo/geoocationNames?zip=8045
  https://api.srgssr.ch/srf-meteo/v2/forecastpoint/47.3587,8.5128
  api.srgssr.ch/srf-meteo/v2/forecastpoint/{47.3587,8.5128}

  /geolocations/{id}

  geolocationID: 
  47.3587,8.5128


  env
VITE_GOOGLE_API_KEY=AIzaSyBnkrLzmcWjKBf7TdGATCrf6SmpfKW_Kjw
VITE_GOOGLE_SHEET_ID=1hzQjE8BH0Ilm8nam7sNRKRyAsd9akxQdKjLz4oBF8is
VITE_SRF_TOKEN=3ulADlktGGVwNiK1yblJ5ElAUU1o