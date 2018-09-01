# Overpass API queries

A collection of useful OVerpass API queries

## Public transport

### Busses

```overpass
[out:xml][timeout:300][bbox:{{bbox}}];
(
  (
    node["highway"="bus_stop"];
    node["public_transport"="platform"]["bus"="yes"];
    node["public_transport"="platform"]["trolleybus"="yes"];
    node["public_transport"="stop_position"]["bus"="yes"];
    node["public_transport"="stop_position"]["trolleybus"="yes"];
  );
  ._;<;
  way["highway"="platform"];
  way["amenity"="shelter"];
  node["amenity"="shelter"];
  relation["route"~"bus|trolleybus"];
);
(._;>;);
out meta;
```

### Trams

```overpass
[out:xml][timeout:300][bbox:{{bbox}}];
(
  (
    node["railway"="tram_stop"];
    node["public_transport"="platform"]["tram"="yes"];
    node["public_transport"="stop_position"]["tram"="yes"];
  );
  ._;<;
  way["railway"="platform"];
  way["building"="station"];
  way["amenity"="shelter"];
  node["amenity"="shelter"];
  relation["route"="tram"];
);
(._;>;);
out meta;
```

### Subway

```overpass
[out:xml][timeout:300][bbox:{{bbox}}];
(
  (
    node["railway"="station"]["station"="subway"];
    node["public_transport"="platform"]["subway"="yes"];
    node["public_transport"="stop_position"]["subway"="yes"];
  );
  ._;<;
  way["railway"="platform"];
  way["building"="station"];
  way["amenity"="shelter"];
  node["amenity"="shelter"];
  relation["route"="subway"];
);
(._;>;);
out meta;
```

### Trains

```overpass
[out:xml][timeout:300][bbox:{{bbox}}];
(
  (
    node["railway"~"station|halt|stop"][!"station"="subway"];
    node["public_transport"="platform"]["train"="yes"];
    node["public_transport"="stop_position"]["train"="yes"];
  );
  ._;<;
  way["railway"="platform"];
  way["building"="station"];
  way["amenity"="shelter"];
  node["amenity"="shelter"];
  relation["route"="train"];
);
(._;>;);
out meta;
```
