# LaTiS Server Test

For some information about LaTiS (and some out-dated code), see https://github.com/dlindhol/LaTiS.

The code for this LaTiS instance can be found at https://github.com/dlindhol/latis-nds. 

After launching this service in NDS Labs, you can use the LaTiS web service API to access an El Nino related index dataset. This LaTiS server instance uses an XML descriptor to **model** a portion of the data source at ftp://ftp.cpc.ncep.noaa.gov/wd52dg/data/indices/sstoi.indices as a LaTiS dataset. In this case I chose to expose the data as a time series (i.e. a **function** of time) of the "Sea Surface Temperature Index - Optimum Interpolation" indices "nino12", "nino3", "nino4", and "nino34".

```
  time -> (nino12, nino3, nino4, nino34)
```

The LaTiS server implements the OPeNDAP (DAP2) specification yet does far more than the typical OPeNDAP server. To get some basic usage information (with lots of rough edges) for this specific instance, see

```
  http://ip:port/latis-nds/latis/
```

To get the full El Nino index dataset (sstoi_indices) in a CSV format:

```
  http://ip:port/latis-nds/latis/sstoi_indices.csv
```

Or in JSON format:

```
  http://ip:port/latis-nds/latis/sstoi_indices.json
```

Or just nino34 for this year with a different time format:

```
  http://ip:port/latis-nds/latis/sstoi_indices.json?time,nino34&time>=2016&format_time(MMM yyyy)
```

LaTiS even models its own log files as a dataset:

```
  http://ip:port/latis-nds/latis/log.txt
```

More to come.