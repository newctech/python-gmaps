# python-gmaps

Google Maps API client.

## Why yet another python google maps client?

There are a bunch of libraries for Google Maps Web Service. To name a few:
* [googlemaps](https://pypi.python.org/pypi/googlemaps/)
* [google.directions](https://pypi.python.org/pypi/google.directions)

What's wrong with them? `googlemaps` uses deprecated google API and forces
you to format your parameters instead of using native python datatypes.
And IMHO is quite incoherent. And `google.directions`? Just take a look
inside it's code...

So here is code using new Google Maps API endpoints. It requires
[requests](https://github.com/kennethreitz/requests), supports native python
datatypes and is sweetened with some syntactic sugar. Nothing more.
No bells and whistles.

Any contributions (code/issues) are welcome.

## Instalation

    pip install python-gmaps

## Usage

Just import API endpoint of your choice and start querying:

```python
from gmaps import Geocoding
api = Geocoding()

api.geocode("somwhere")
api.reverse(51.123, 21.123)
```

If you need to use Google Maps API for Business then instantiate your endpoint
with `api_key` param

```python
from gmaps import Geocoding
api = Geocoding(api_key='your_secret_api_key`)
```

Each endpoint method raises adequate exception when status of query is different
than `OK`. It also unpacks results list from Google API output dict so you have
one key less to access but it does nothing more.
So if Google geocoding api outputs something like:

```json
{
    results: [
    ...
    ],
    status: 'OK'
}
```

You will get only get list that was inside `result` value. At least one element
returned is always assured, otherwise `gmnaps.errors.NoResults` exception is
raised.

For each API endpoint you can specify:
* default `sensor` value
* protocol (http/https)
* api key (only for http)

Available endpoints:
* `Geocoding()`

For detailed documentation of each endpoint refer to dosctrings. If you need
list of available values for some parameters (like geocoding components,
languages, regions etc.) refer to
[Google Maps API docs](https://developers.google.com/maps/documentation/webservices/).
These values can change anytime so there is no reason to check for them in this
lib - they will be checked anyway.

## Changes

### 0.0.2 (TBA)
- `Directions` endpoint added

### 0.0.1 (2013-10-03)
- initial release
- ```Geocoding``` endpoint