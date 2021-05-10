# NOAA GHCN-D

This dataset contains weather observations for over 200 years of a large number
of land-based weather measurement stations, sourced
from the [Registry of Open Data on AWS (RODA)](https://registry.opendata.aws/noaa-ghcn/);

### Source

 * Website: https://registry.opendata.aws/noaa-ghcn/
 * Readme: https://docs.opendata.aws/noaa-ghcn-pds/readme.html

### Tables

 1. **noaa_ghcn_pds.observations** Weather observations
 2. **noaa_ghcn_pds.stations** Weather stations
 3. **noaa_ghcn_pds.countries** Country locations for weather stations
 4. **noaa_ghcn_pds.states** State locations for weather stations

### Samples

Here is a sample query that shows the days it snowed in virginia during the
last year by different observation points.

```
select s.name, o.year_date, count(*)
from noaa_ghcn_pds.observations o
join noaa_ghcn_pds.stations s
on o.id = s.id
where o.year_date >= 10000 * extract(year from current_timestamp)::int
and o.element = 'SNOW'
and s.state = 'VA'
and o.data_value > 0
group by 1, 2
order by 1, 2
```
