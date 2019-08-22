#Osm label server  [![Build Status](https://travis-ci.org/trump-fmi/osm_label_server.svg?branch=master)](https://travis-ci.org/trump-fmi/osm_label_server)

Tool for serving OpenstreetMap (osm) points with a description label independet of the map tiles. The main purpose is serving the labels for rotation independent labeling of osm maps. It relies the data and api provided by the [runtime_datastructure](https://github.com/trump-fmi/runtime_datastructure) project. Datasets have to be provided in its format to be accesses by the osm label server. 

## Functions
The tool stats a server and answers requests at default at `/label/<endpoint>` with a geojson of the requested points. The request contains a bounding box and additional parameter for a selection of points to include. 
Example request (which requests all labels with *t_min* larger than 0.1): 
```http
GET http://localhost:8080/label/citynames?x_min=0&x_max=180&y_min=0&y_max=180&t_min=0.1
```
### Endpoint parameters 
The current parameters allow the setting of the bounding box and a filtering t value. The ordering as displayed in the example has to be used. 
* *x_min*, *x_max*, *y_min* and *y_max* define the bounding box
* *t_min* allows only points with a t value larger than the given value

### Response
The response is in the [Geojson format](http://geojson.org/). An example with one label is provided below:
``` json
{"type":"FeatureCollection","features":[{"type":"Feature","geometry":{"type":"Point","coordinates":[8.7422973,53.051944500000005]},"properties":{"lbl_fac":26,"name":"Huchting","osm":30349113,"prio":121,"t":0.7067380674933035}}],"crs":{"type":"name","properties":{"name":"urn:ogc:def:crs:OGC:1.3:CRS84"}}}

```

## Installation

For installation please refer to the github pages of the [TRUMP OSM Label Server](https://github.com/trump-fmi/osm_label_server).


## Configuration 
The startup can be configured with parameters flags. 

### Flags
Flags can be set by "-flag value" or "-flag=value". If you want to keep the defaults, you do not have to supply anything. 

| Flag       | Default value | Explanation                                        |
|------------|---------------|----------------------------------------------------|
| -endpoints | default.json  | Path to the file with the endpoint configurations. |
| -port      | 8080          | Port where the socket is opened.                   |
| -root      | label         | Root endpoint for the label providing endpoints.   |

### Configuration file
The endpoint configuration is stored as json. For each endpoint the name and a path to a file is stored. The file contains the labels which should be provided at the endpoint. 
