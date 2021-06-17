# [Google Places for Flutter](https://pub.dev/packages/google_places_for_flutter)

A Flutter package which uses the Google Maps API to make a TextField that tries to autocomplete places as the user types, with simple smooth animations, providing a nice UI and UX. This will also provide great information about the user selected place, like the coordinates, the bounds to determine the zoom of the GoogleMap widget, and so on.

Extended [Google Maps for Flutter](https://pub.dev/packages/google_maps_flutter) plugin

[![pub package](https://img.shields.io/pub/v/google_places_for_flutter.svg)](https://pub.dev/packages/google_places_for_flutter)


## Installation

``` flutter pub add google_places_for_flutter ```

or


```
dependencies:
  google_places_for_flutter: ^1.0.0

```

```dart

import 'package:google_places_for_flutter/google_places_for_flutter.dart';

SearchGooglePlacesWidget(
    placeType: PlaceType.address, // PlaceType.cities, PlaceType.geocode, PlaceType.region etc
    placeholder: 'Enter the address',
    apiKey:
        'Your Google Map API Key goes here',
    onSearch: (Place place) {},
    onSelected: (Place place) async {
      print('address ${place.description}');
      
    },
),
```

```dart
SearchGooglePlacesWidget(
    apiKey: 'Your Google Map API Key goes here',
    // The language of the autocompletion
    language: 'en',
    // The position used to give better recomendations. In this case we are using the user position
    location: userPosition.coordinates,
    radius: 30000,
    onSelected: (Place place) async {
        final geolocation = await place.geolocation;

        // Will animate the GoogleMap camera, taking us to the selected position with an appropriate zoom
        final GoogleMapController controller = await _mapController.future;
        controller.animateCamera(CameraUpdate.newLatLng(geolocation.coordinates));
        controller.animateCamera(CameraUpdate.newLatLngBounds(geolocation.bounds, 0));
    },
);
```