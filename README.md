## Graphite + Carbon + Whisper (*Version: 1.1.5*)

An all-in-one image running graphite, carbon-cache and a whisper database.

This image contains a default configuration of graphite and carbon-cache.
Starting this container will, by default, bind the the following host ports:

- `8080`: the graphite web interface
- `2003`: the carbon-cache line receiver
- `2004`: the carbon-cache pickle receiver
- `7002`: the carbon-cache query port

You can log into the administrative interface of graphite-web with
the username `admin` and password `admin`.
These passwords can be changed through the web interface.

**NB**: Please be aware that by default docker will make the exposed ports
accessible from anywhere if the host firewall is unconfigured.

### Data volumes

Graphite data are stored at `/var/lib/graphite/storage/whisper` within the
container.
If you want to store your metrics outside the container (for persistence)
you can use docker's data volumes feature.

Graphite configuration is stored at `/var/lib/graphite/conf/` within the
container.
If you want to provide your own persistent configuration you can
use docker's data volumes feature.

All logs are stored in `/var/log/` within the container.
If you want to persist them you can use docker's data volumes feature.

For example, to:

- store graphite's metric database at `/data/graphite` on the host
- use graphite's configuration at `/conf/graphite` on the host
- store container's logs at `/log/graphite` on the host

you can run:

    docker run --name graphite \
               -v /data/graphite:/var/lib/graphite/storage/whisper \
               -v /conf/graphite:/var/lib/graphite/conf/ \
               -v /log/graphite:/var/log/ \
               -d sixsq/graphite-container

### Defaults

By default, this instance of carbon-cache uses the following retention periods
resulting in whisper files of approximately 4MiB.

    60s:30d,5m:183d,15m:2y,30m:5y,1h:10y

By default, the timezone is configured to `Europe/Zurich`.
To change it, edit the following file in the container:
`/var/lib/graphite/webapp/graphite/local_settings.py`


## Copyright

Copyright &copy; 2021, SixSq SA
