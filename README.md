# WoBike

Documentation of Bike Sharing APIs

Public transport and multimodal routing apps could benefit from showing nearby bikes from bikesharing services. So here's a list showing the APIs of a few of these platforms.

## Nextbike (Worldwide)

### API

URL: `https://api.nextbike.net/maps/nextbike-live.json` as JSON or `https://api.nextbike.net/maps/nextbike-live.xml` as XML. You also can filter by city, with the GET-Parameter `city`. Eg `https://api.nextbike.net/maps/nextbike-live.json?city=362` for Berlin.

For some cities nextbike has flexzones (free floating in these zones). At the moment these are:

* Köln `https://api.nextbike.net/reservation/geojson/flexzone_kg.json`
* Berlin `https://api.nextbike.net/reservation/geojson/flexzone_bn.json`
* Dresden `https://api.nextbike.net/reservation/geojson/flexzone_sz.json`
* Karlsruhe `https://api.nextbike.net/reservation/geojson/flexzone_fg.json`
* Nürnberg `https://api.nextbike.net/reservation/geojson/flexzone_nb.json`
* For all zones: `https://api.nextbike.net/reservation/geojson/flexzone_all.json`

### GBFS

Nextbike provides different GBFS endpoints for their different networks/brands/countries:
`https://api.nextbike.net/maps/gbfs/v1/nextbike_<NETWORK-ID>/gbfs.json`. You can find the Network-ID in the `https://api.nextbike.net/maps/nextbike-live.json`, just search for the `"domain"` JSON Key in country root object. So GBFS endpoint for Germany would be `https://api.nextbike.net/maps/gbfs/v1/nextbike_de/gbfs.json`. Warning: Not all german citys are in the `de` endpoint, e.g. in Berlin nextbike partnered with Deezer and uses Network-ID/country code `bn`.

## Call-a-Bike (Germany / Deutsche Bahn)

Call-a-Bike has [historic datasets](http://data.deutschebahn.com/dataset/data-call-a-bike) OpenData on the DeutscheBahn OpenData portal under CC-BY License.

You can use the [Flinkster API](http://data.deutschebahn.com/dataset/flinkster-api) with `providernetwork=2` to access Call-a-Bike live Data. You need to register on [developer.deutschebahn.com](https://developer.deutschebahn.com/store/site/pages/sign-up.jag) to get a free, unlimited API Key (Zugangstoken).

Example Request: `https://api.deutschebahn.com/flinkster-api-ng/v1/bookingproposals?lat=48.15&lon=11.5&radius=5000&limit=100&providernetwork=2` – You also have to set the `Authorization` header to `Bearer <YOUR-API-KEY>`

* Paramter `limit` max value is `100`, but you can use `offset` to request more
* Paramter `radius` is the searchradius in meters, max value is `10000`, min value is `100`, default `500`,
* You can also add parameter `expand` to `rentalobject,price` to get vehicle and price info

There is also a [Documentation PDF](https://developer.deutschebahn.com/store/site/themes/responsive/templates/api/documentation/download.jag?tenant=carbon.super&resourceUrl=/registry/resource/_system/governance/apimgt/applicationdata/provider/DBOpenData/Flinkster_API_NG/v1/documentation/files/Schnittstellenspezifikation_FlinksterApiNG.pdf) (german only), and you can use the [API-console (3rd tab)](https://developer.deutschebahn.com/store/apis/info?name=Flinkster_API_NG&version=v1&provider=DBOpenData)

If you need GBFS, maybe this [flinkster2gbfs](https://github.com/mfdz/flinkster2gbfs) adapter can help.

## oBike (Worldwide)

[Detailed documentation](Obike.md)

## ofo bike (China, UK, US, Austria, Thailand, Singapore, France, India)

[Detailed documentation](Ofo.md)

## mobike

[Detailed documentation](Mobike.md)

## yobike/ohbike/indigo wheel

Yobike (ex ohbike) sell their systems under white label.
Only the Application key differ

[Detailed documentation](Yobike.md)

## Gobee bike (Hong Kong, France, Belgium, Italy)

Simple GET-Request example: `https://appaws.gobee.bike/GobeeBike/bikes/near_bikes?accuracy=20&lat=22.38&lng=114.198`
Alternative endpoint: `https://api.gobee.bike/`

## bluegogo (China, US)

POST-Request to `https://api-us.bluegogo.com/nearbyBikes?data={"token":"","version":1,"data":{"latitude":22.5526,"longitude":114.1029,"billingModelIds":"1,2,3"}}`

(The JSON should be URLencoded.) – If the token is empty, the bikelist will also be empty. I guess you get a token when signing in.

## LimeBike

[Detailed documentation](Lime.md)

## Motivate (US)

[Motivate](https://www.motivateco.com/) builds Bikesharing Systems. They publish their [Data and APIs](https://www.motivateco.com/use-our-data/). This includes the following systems (cities) in the US:

* Ford GoBike (Bay Area, CA)
  * GBFS: `https://gbfs.fordgobike.com/gbfs/gbfs.json`
* Biketown (Portland, OR)
* Capital Bikeshare (Washington, DC)
* Bike Chattanooga (Chattanooga, TN)
* Citi Bike (New York)
* CoGo (Columbus, OH)
* Divvy (Chicago, IL)
* Hubway (Boston, MA)

All APIs and data are also listed on `https://www.motivateco.com/use-our-data/`

Motivate also has undocumented APIs in the GeoJSON format. URLs might be tricky to divine for other cities, but Washington DC & NYC are:
 * https://layer.bicyclesharing.net/map/v1/wdc/map-inventory
 * https://layer.bicyclesharing.net/map/v1/nyc/map-inventory

## BYKE (Germany)

Simple GET-Request example: `https://api-prod.ibyke.io/v1/bikes?latitude=52.55001&longitude=13.40902&order=nearby`

## dropbike (Canada)

* `POST`-Request: `https://dropbikeadminapi.herokuapp.com/v1/bikes_nearby`
* (Header `Content-Type` to `application/json`)
* Request Payload example: `{"lat":43.659415191015498,"lng":-79.395512826740742}`

* You can also get their regions with a simple `POST`-Request (without payload) to `https://dropbikeadminapi.herokuapp.com/v1/region_polygons`

## JUMP (USA)

[JUMP](http://jumpbikes.com/) operates electric dockless bikeshares in Washington, DC & San
Francisco. They operate open data APIs at https://dc.jumpmobility.com/opendata
and https://sf.jumpbikes.com/opendata respectively.

Also see https://github.com/Leschonander/Jump-Bike-D.C-Python-API-Wrapper

## SocialBicycles (USA, Canada, Czech Republic, Poland)

[SocialBicycles](http://socialbicycles.com/) is JUMP's partership-based bikeshare program. They publish their [Data and APIs](https://app.socialbicycles.com/developer/#!/networks). This includes the following systems (cities) around the world:

* Atlanta, Boise, Charlottesville, Eugene, New Orleans, Orlando, Phoenix, Portland, Santa Monica, Tampa (USA)
* SoBi Hamilton (Hamilton, ON, CA)
* Velonet (Czech Republic)
* Wavelo (Warsaw, Poland)
* many more..

## OnzO (New Zealand)

Simple GET request: https://app.onzo.co.nz/nearby/-36.848123/174.765588/50.0

[Detailed documentation](Onzo.md)

## Spin (Bikes and Scooter)

[Spin](https://www.spin.pm/) is a Bike and E-Scotter sharing service in the US.

[Detailed documentation](Spin.md)

## Bird (Scooter)

[Bird](https://www.bird.co/) is a E-Scotter sharing service in the US.

[Detailed documentation](Bird.md)

## Bixi (Montréal, QC, Canada)

A GET request to:

```
https://layer.bicyclesharing.net/map/v1/mtl/stations
```

yields a response looking like:

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [
          -73.55650842189789,
          45.51035067563653
        ]
      },
      "properties": {
        "station_id": "1",
        "name": "Métro Champ-de-Mars (Sanguinet / Viger)",
        "terminal": "6001",
        "capacity": 33,
        "bikes_available": 11,
        "docks_available": 22,
        "bikes_disabled": 0,
        "docks_disabled": 0,
        "renting": true,
        "returning": true,
        "installed": true,
        "last_reported": 1533227391,
        "icon_pin_bike_layer": "pin-bike-green-half",
        "icon_pin_dock_layer": "pin-dock-green-most",
        "icon_dot_bike_layer": "dot-green",
        "icon_dot_dock_layer": "dot-green",
        "valet_status": "none"
      }
    }
  ]
}
```

The array of "Features" contains status on each Bixi bike sharing station in Montréal.

## Zagster

List of all cities: https://zapi.zagster.com/api/v1/bikeshares/

For more information about bikes in a specific city, you'll need the city ID (found in `metadata["data"]["_id"]` from the above link)

List of stations in a city and station metadata: `https://zapi.zagster.com/api/v1/bikeshares/[City ID]/stations`

List of bikes in a city and bike metadata: `https://zapi.zagster.com/api/v1/bikeshares/[City ID]/bikes`

## EUBIKE (Sweden)

[EUBIKE](http://eubike.se) is a Swedish bike rental company with dock-less rentals. The user scans a QR-code located on the bike´s lock to unlock it. To perform a simply search for bikes, you can send a POST request to this URL:
`http://47.91.87.181:8080/UserApi/AppUser?lng=18.0668918788433075&lat=59.3109666242335791&cmd=areabike&dist=0.5`
The IP address is an Alibaba Cloud Server located in Germany used by the EUBIKE mobile app itself.
A sample response for the request above is:
`{"success":true,"data":[{"devid":"10002165","shebeistatus":0,"devlat":59.31163,"devlng":18.06885,"devpower":0,"dist":0.133420259},{"devid":"10000991","shebeistatus":0,"devlat":59.30986,"devlng":18.06548,"devpower":0,"dist":0.147037461},{"devid":"10001231","shebeistatus":0,"devlat":59.3098221,"devlng":18.0654163,"devpower":0,"dist":0.15217796},{"devid":"10001958","shebeistatus":0,"devlat":59.3130035,"devlng":18.0675964,"devpower":0,"dist":0.230080515},{"devid":"10001357","shebeistatus":0,"devlat":59.31213,"devlng":18.0620575,"devpower":0,"dist":0.303918362},{"devid":"10002477","shebeistatus":0,"devlat":59.3123932,"devlng":18.0622749,"devpower":0,"dist":0.306723356}...],"maparea" : []`

This endpoint is more well-documented in the file 
[EUBike.md](EUBike.md).

## VOI (Scooter, Europe)
[VOI](https://voiscooters.com) is a scooter sharing company founded in Sweden. They have electric scooters available at several locations in Europe, including cities in Sweden, Spain, Italy, France and others. A simple GET request to get scooters available for rental nearby a location (specified with latitude/longtitude parameters) looks like this:

`https://api.voiapp.io/v1/vehicle/status/ready?lat=59.329323&lng=18.068581`

(**no authentication is needed**)

The request will return data about scooters in a list with JSON objects. More detailed documentation as well as an explaination of most of the request and response parameters can be found in the file [Voi.md](Voi.md).

## Flash / Circ (Scooter)

[Detailed documentation](Flash.md) 

## Helbiz (Scooter)

[Detailed documentation](Helbiz.md) 

## Hive (Scooter, Europe)
[hive](https://www.ridehive.com) is a scootersharing company based in Europe.

There is *no* authentication or special headers and only `GET`-Requests required for the API-Endpoint `https://hive.frontend.fleetbird.eu/api/prod/v1.06/`. You can request all(?) vehicles with `https://hive.frontend.fleetbird.eu/api/prod/v1.06/map/cars/` or filter them by bbox like `https://hive.frontend.fleetbird.eu/api/prod/v1.06/map/cars/?lat1=46.8339&lat2=55.829&lon1=4.205&lon2=27.653` or show the 20 nearest vehicles around a location with `https://hive.frontend.fleetbird.eu/api/prod/v1.06/cars/?lat=53.4374&lon=9.9955`.

Polygons with regions and parking restrictions are available on `https://hive.frontend.fleetbird.eu/api/prod/v1.06/territories/all/` (`type: 0` looks like free floating region and `type: 1` are no parking zones).

Vehicle types with images are available on `https://hive.frontend.fleetbird.eu/api/prod/v1.06/cars/types/`

## TIER (Scooter, Europe, UAE)
[tier](https://www.tier.app/) is a scootersharing company based in Europe.

To authenticate you need to add `X-Api-Key: bpEUTJEBTf74oGRWxaIcW7aeZMzDDODe1yBoSxi2` in your header of the API-Endpoint `https://platform.tier-services.io`. You can request all(?) vehicles with `https://platform.tier-services.io/vehicle?` or filter them by zoneID like `https://platform.tier-services.io/vehicle?zoneId=BERLIN` or show all the vehicles around a location with a given radius (meters) `https://platform.tier-services.io/vehicle?lat=0&lng=0&radius=500`.

Polygons with regions and parking restrictions are available on `https://platform.tier-services.io/zone?lat=55.605&lng=13.0038`.

## Ufo (Scooter, Europe)
[Ufo](https://www.ufoscooters.com/) is a scootersharing company based in Europe.

There is *no* authentication or special headers and only `GET`-Requests required for the API-Endpoint `https://ufo.frontend.fleetbird.eu/api/prod/v1.06/`. You can request all(?) vehicles with `https://ufo.frontend.fleetbird.eu/api/prod/v1.06/map/cars/` or filter them by bbox like `https://ufo.frontend.fleetbird.eu/api/prod/v1.06/map/cars/?lat1=35.0&lat2=44.0&lon1=-35.0&lon2=4.0` or show the 20 nearest vehicles around a location with `https://ufo.frontend.fleetbird.eu/api/prod/v1.06/cars/?lat=40.4021&lon=-3.6857`.

Polygons with regions and parking restrictions are available on https://ufo.frontend.fleetbird.eu/api/prod/v1.06/territories/all/ (type: 0 looks like free floating region and type: 1 are no parking zones).

Vehicle types with images are available on https://ufo.frontend.fleetbird.eu/api/prod/v1.06/cars/types/

## Zero (Scooter, Germany)
[Zero](https://gozero.eco/de/) is a scootersharing company based in Germany.

There is *no* authentication or special headers and only `GET`-Requests required for the API-Endpoint `https://zero.frontend.fleetbird.eu/api/prod/v1.06/`. You can request all(?) vehicles with `https://zero.frontend.fleetbird.eu/api/prod/v1.06/map/cars/` or filter them by bbox like `https://zero.frontend.fleetbird.eu/api/prod/v1.06/map/cars/?lat1=46.8339&lat2=55.829&lon1=4.205&lon2=27.653` or show the 20 nearest vehicles around a location with `https://zero.frontend.fleetbird.eu/api/prod/v1.06/cars/?lat=53.4374&lon=9.9955`.

Polygons with regions and parking restrictions are available on `https://zero.frontend.fleetbird.eu/api/prod/v1.06/territories/all/` (`type: 0` looks like free floating region and `type: 1` are no parking zones).

Vehicle types with images are available on `https://zero.frontend.fleetbird.eu/api/prod/v1.06/cars/types/`

## Scoota (Scooter, Austria)
[Scoota](https://www.scoota.online/) is a scootersharing company based in Austria.

There is *no* authentication or special headers and only `GET`-Requests required for the API-Endpoint `https://scoota.frontend.fleetbird.eu/api/prod/v1.06/`. You can request all(?) vehicles with `https://scoota.frontend.fleetbird.eu/api/prod/v1.06/map/cars/` or filter them by bbox like `https://scoota.frontend.fleetbird.eu/api/prod/v1.06/map/cars/?lat1=46.8339&lat2=55.829&lon1=4.205&lon2=27.653` or show the 20 nearest vehicles around a location with `https://scoota.frontend.fleetbird.eu/api/prod/v1.06/cars/?lat=46.6231&lon=14.3080`.

Polygons with regions and parking restrictions are available on `https://scoota.frontend.fleetbird.eu/api/prod/v1.06/territories/all/` (`type: 0` looks like free floating region and `type: 1` are no parking zones).

Vehicle types with images are available on `https://scoota.frontend.fleetbird.eu/api/prod/v1.06/cars/types/`

## Emmy (🛵 Electric Motorbikes, Germany)
[Emmy](https://emmy-sharing.de/) is a german rental service for electric motorbikes 🛵 (also called scooter, the wording is a mess).

There is *no* authentication or special headers and only `GET`-Requests required for the API-Endpoint `https://emmy.frontend.fleetbird.eu/api/prod/v1.06/`. You can request all(?) vehicles with `https://emmy.frontend.fleetbird.eu/api/prod/v1.06/map/cars/` or filter them by bbox like `https://emmy.frontend.fleetbird.eu/api/prod/v1.06/map/cars/?lat1=46.8339&lat2=55.829&lon1=4.205&lon2=27.653` or show the 20 nearest vehicles around a location with `https://emmy.frontend.fleetbird.eu/api/prod/v1.06/cars/?lat=53.4374&lon=9.9955`.

Polygons with regions and parking restrictions are available on `https://emmy.frontend.fleetbird.eu/api/prod/v1.06/territories/all/` (`type: 0` looks like free floating region and `type: 1` are no parking zones).

Vehicle types with images are available on `https://emmy.frontend.fleetbird.eu/api/prod/v1.06/cars/types/`

## Coup (🛵 Electric Motorbikes, Germany, Spain, France)
[Coup](https://www.joincoup.com/) is a rental service for electric motorbikes 🛵 (also called scooter, the wording is a mess).

First request the cities with `GET` request `https://app.joincoup.com/api/v3/markets`. Get the `id` for your city and request all vehicles with a `GET` request `https://app.joincoup.com/api/v3/markets/{id}/scooters` for example for Berlin: `https://app.joincoup.com/api/v3/markets/fb7aadac-bded-4321-9223-e3c30c5e3ba5/scooters`. A `GET` request to
`https://app.joincoup.com/api/v3/markets/{id}/business_areas` will give you business areas for that city.



## More...

* Also have a look at [this project](https://github.com/eskerda/pybikes/tree/master/pybikes)
* [GBFS (General Bikeshare Feed Specification)](https://github.com/NABSA/gbfs)
* [Bikesharing World Map](https://www.google.com/maps/d/u/0/viewer?mid=1UxYw9YrwT_R3SGsktJU3D-2GpMU&ll=50.01042750703113%2C35.03132237929685&z=2)
* [Open Bike Share Data](https://bikeshare-research.org/)

## Todo

* [Pony Bikes](http://getapony.com/) (uses certificate pinning)
* [Donkey Republic](http://www.donkey.bike/) (uses certificate pinning)
