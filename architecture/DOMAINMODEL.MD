# Main concepts

## Forecast model

Weacast aims at gathering, exposing, and making use of weather forecast data generated by **forecast models**. It does often exist different **instances** of a forecast model producing more or less accurate data, usually in term of spatial or temporal resolution. As an example the [GFS](https://www.ncdc.noaa.gov/data-access/model-data/model-datasets/global-forcast-system-gfs) model produces data at 1° or 0.5° degree of resolution with different time steps (e.g. each 3 hours until the production time + 240 hours). The production of a set of forecast data is called a **run** of the model and occurs on a regular daily basis, e.g. every 6 hours.

The spatial properties of a model instance are completely defined by a [grid](https://weacast.gitbooks.io/weacast-docs/api/GRID.html). The temporal properties are defined by interval values describing at which frequency/time the forecast data are produced (so called **run interval/time**) and which time steps are available (so called **forecast interval/time**).

## Forecast element

Each configured forecast model instance output hundreds of **forecast elements** (i.e. meteorological elements) such as temperature, wind direction, etc. Forecast data are continuously updated because the model instance produces new forecast data for its elements every N hours.

## Probe

**Probes** are virtual sensors used to probe forecast data at specific locations of interest (e.g. airports, cities, stores, etc.). It does exist two kind of probes:
* **on-demand probing**, which allow to compute *on-demand* forecast element values for a given forecast time and a set of locations,
* **probing stream**, which allow to automatically and continuously compute forecast element values for a set of locations as new forecast data are gathered.

> Probed values are computed using [interpolation](../api/GRID.MD#interpolatelongitude-latitude) of the forecast data

## Probe results querying

While on-demand probing directly returns the results you asked for, probing streams generates the results continuously without your intervention. We thus need a way to query the persisted results on-demand using:
* **selectors**: to find all results where an attribute has (or does not have) the specified value (e.g. forecast time);
* **comparison operators**: to find all results where the target element value is less, less or equal, greater, greater or equal than a given value;
* **spatial operators**: to find all results located within a given geometry on the ground (e.g. in a given radius around a point).

# Domain model

The **domain model** is a set of high-level abstractions that describes selected aspects of a sphere of activity, more specifically [numerical weather prediction](https://en.wikipedia.org/wiki/Numerical_weather_prediction) for Weacast. It is a representation of meaningful real-world concepts pertinent to the domain that are modeled in the software. The concepts include the data involved in the business and rules the business uses in relation to that data.

The class diagram used to represent the domain model in the [Unified Modeling Language](https://en.wikipedia.org/wiki/Unified_Modeling_Language) (UML) is presented afterwards. The Weacast domain model is implemented as a hybridation between [objects](https://en.wikipedia.org/wiki/Object-oriented_programming) and [cross-cutting concerns](https://en.wikipedia.org/wiki/Aspect-oriented_software_development) within a layer that uses a lower-level layer for [persistence](./DATAMODEL.MD) and *publishes* an [API](../api/README.MD) to a higher-level layer to gain access to the data and behavior of the model. 

![Domain model](https://cdn.rawgit.com/weacast/weacast-docs/49febdcdf850d447be0e8a5bae335f4f75db6dd9/images/Domain%20Model%20Diagram.svg)

To get into the details of this model look at the [persisted data model](./DATAMODEL.MD) and the provided [API](../api/README.MD).

