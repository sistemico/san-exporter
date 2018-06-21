# San Exporter

A small library which allows to push data to Santimen data processing pipelines.

## Writing exporters

When writing data exporter you need to make sure the following things:

* All the logging should be on the stdout. Do not create any temp files, as they
will most probably disappear in an event of a restart
* All the config should come from ENV variables
* An exporter should continue from where it was interrupted in case of a restart.
You can save the current position using the `savePosition(position)` API.
* Encode the data as JSON

See `examples/send_dates.js` for an example how to build an exporter that sends
the current date every 10 sec. You can run the example with `docker-compose`:

```bash
$ docker-compose up --build
```

This is going to ensure that all dependent services are created.

## API

* `connect` - establish connection to the dependent services. Returns a Promise
* `getLastPosition` - fetch the last saved position. Returns a Promise
* `savePosition` - update the last position of the exporter. Returns a Promise
* `sendData` - push an array of events. Returns a Promise