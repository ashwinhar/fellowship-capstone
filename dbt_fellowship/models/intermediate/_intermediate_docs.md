{% docs int_hourly_ridership_timestamp_parts %}

Partitions the `transit_timestamp` column using DuckDB's `date_part` function
such that we can eventually achieve the same grain as `fct_origin_destination`

{% enddocs %}


{% docs int_ada_complexes %}

Filters to all complexes in `stg_stations` that have at least one record where `ada = 1`. 
Brings all lines in the complex and station names into a list. 

{% enddocs %}


{% docs int_origin_destination_ada %}

Filters origin and destination to all combinations where both `origin_station_complex_id` and
`destination_station_complex_id` are in `int_ada_complexes.ada_complex_id`. In other words,
filters the table to all records where both the origin and destination are accessible.

{% enddocs %}


{% docs int_hourly_ridership_filteraggregate %}

Aggregates `hourly_ridership` into the same grain as `origin_destination` but instead of *averaging*
the ridership it totals the ridership. This way, we don't lose information.

{% enddocs %}