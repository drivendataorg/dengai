# Problem description

Your goal is to predict the `total_cases` label for each `(city, year, weekofyear)` in the test set. There are two cities, San Juan and Iquitos, with test data for each city spanning 5 and 3 years respectively. You will make one submission that contains predictions for both cities. The data for each city have been concatenated along with a `city` column indicating the source: `sj` for San Juan and `iq` for Iquitos. The test set is a pure future hold-out, meaning the test data are sequential and non-overlapping with any of the training data.  Throughout, missing values have been filled as `NaN`s.

<div class="container">
  <div class="row">
    <div class="col-xs-3">
      <ul style="list-style: none">
        <li><strong>Features</strong></li>
        <li><a href="#features_list">List of features</a></li>
        <li><a href="#features_eg">Example of features</a></li>
      </ul>
    </div>
    <div class="col-xs-3">
      <ul style="list-style: none">
        <li><strong>Performance metric</strong></li>
        <li><a href="#mae">Mean absolute error</a></li>
      </ul>
    </div>
    <div class="col-xs-3">
      <ul style="list-style: none">
        <li><strong>Submission Format</strong></li>
        <li><a href="#sub_values">Format example</a></li>
      </ul>
    </div>
  </div>
</div>

<a id="features_list"></a>

## The features in this dataset

-----

You are provided the following set of information on a `(year, weekofyear)` timescale:

(Where appropriate, units are provided as a `_unit` suffix on the feature name.)

### City and date indicators
* `city` – City abbreviations: `sj` for San Juan and `iq` for Iquitos
* `week_start_date` – Date given in yyyy-mm-dd format

### NOAA's GHCN [daily climate data](https://www.ncdc.noaa.gov/oa/climate/ghcn-daily/) weather station measurements
* `station_max_temp_c` – Maximum temperature
* `station_min_temp_c` – Minimum temperature
* `station_avg_temp_c` – Average temperature
* `station_precip_mm` – Total precipitation
* `station_diur_temp_rng_c` – Diurnal temperature range

### PERSIANN [satellite precipitation measurements](http://www.ncdc.noaa.gov/cdr/operationalcdrs.html) (0.25x0.25 degree scale)
* `precipitation_amt_mm` – Total precipitation

### NOAA's NCEP [Climate Forecast System Reanalysis](http://rda.ucar.edu/datasets/ds093.0/#metadata/detailed.html?_do=y) measurements (0.5x0.5 degree scale)
* `reanalysis_sat_precip_amt_mm` – Total precipitation
* `reanalysis_dew_point_temp_k` – Mean dew point temperature
* `reanalysis_air_temp_k` – Mean air temperature
* `reanalysis_relative_humidity_percent` – Mean relative humidity
* `reanalysis_specific_humidity_g_per_kg` – Mean specific humidity
* `reanalysis_precip_amt_kg_per_m2` – Total precipitation
* `reanalysis_max_air_temp_k` – Maximum air temperature
* `reanalysis_min_air_temp_k` – Minimum air temperature
* `reanalysis_avg_temp_k` – Average air temperature
* `reanalysis_tdtr_k` – Diurnal temperature range

### Satellite vegetation - Normalized difference vegetation index (NDVI) - NOAA's [CDR Normalized Difference Vegetation Index](https://www.ncdc.noaa.gov/cdr) (0.5x0.5 degree scale) measurements
* `ndvi_se` – Pixel southeast of city centroid
* `ndvi_sw` – Pixel southwest of city centroid
* `ndvi_ne` – Pixel northeast of city centroid
* `ndvi_nw` – Pixel northwest of city centroid


<a id="features_eg"></a>

<div class="well">

<h3> Feature data example</h3>

<hr/>

For example, a single row in the dataset, indexed by (city, year, weekofyear): (sj, 1994, 18), has these values:
<br/>
<br/>

<table style="width:70%; margin-left:15%; margin-right:15%;" class="table">
  <tbody>
    <tr>
      <th>week_start_date</th>
      <td>1994-05-07</td>
    </tr>
    <tr>
      <th>total_cases</th>
      <td>22</td>
    </tr>
    <tr>
      <th>station_max_temp_c</th>
      <td>33.3</td>
    </tr>
    <tr>
      <th>station_avg_temp_c</th>
      <td>27.7571428571</td>
    </tr>
    <tr>
      <th>station_precip_mm</th>
      <td>10.5</td>
    </tr>
    <tr>
      <th>station_min_temp_c</th>
      <td>22.8</td>
    </tr>
    <tr>
      <th>station_diur_temp_rng_c</th>
      <td>7.7</td>
    </tr>
    <tr>
      <th>precipitation_amt_mm</th>
      <td>68.0</td>
    </tr>
    <tr>
      <th>reanalysis_sat_precip_amt_mm</th>
      <td>68.0</td>
    </tr>
    <tr>
      <th>reanalysis_dew_point_temp_k</th>
      <td>295.235714286</td>
    </tr>
    <tr>
      <th>reanalysis_air_temp_k</th>
      <td>298.927142857</td>
    </tr>
    <tr>
      <th>reanalysis_relative_humidity_percent</th>
      <td>80.3528571429</td>
    </tr>
    <tr>
      <th>reanalysis_specific_humidity_g_per_kg</th>
      <td>16.6214285714</td>
    </tr>
    <tr>
      <th>reanalysis_precip_amt_kg_per_m2</th>
      <td>14.1</td>
    </tr>
    <tr>
      <th>reanalysis_max_air_temp_k</th>
      <td>301.1</td>
    </tr>
    <tr>
      <th>reanalysis_min_air_temp_k</th>
      <td>297.0</td>
    </tr>
    <tr>
      <th>reanalysis_avg_temp_k</th>
      <td>299.092857143</td>
    </tr>
    <tr>
      <th>reanalysis_tdtr_k</th>
      <td>2.67142857143</td>
    </tr>
    <tr>
      <th>ndvi_location_1</th>
      <td>0.1644143</td>
    </tr>
    <tr>
      <th>ndvi_location_2</th>
      <td>0.0652</td>
    </tr>
    <tr>
      <th>ndvi_location_3</th>
      <td>0.1321429</td>
    </tr>
    <tr>
      <th>ndvi_location_4</th>
      <td>0.08175</td>
    </tr> </tbody>
</table>

</div>

<a id="mae"></a>

## Performance metric

-----

Performance is evaluated according to the [mean absolute error](https://en.wikipedia.org/wiki/Mean_absolute_error).

<a id="sub_cols"></a>

## Submission format

-----

The format for the submission file is simply the `(city, year, weekofyear)` and the predicted `total_cases` for San Juan or Iquitos (for an example, see `SubmissionFormat.csv` on the data download page). The `total_cases` should be represented as integer values.

<a id="sub_values"></a>

<div class="well">

For example, if you just predicted that there were 5 cases each week for 5 weeks in San Juan and 3 cases each week for 5 weeks in Iquitos, for a total of 10 weeks, you would have the following predictions:

<table class="table">
<thead>
  <tr style="text-align: right;">
    <th>city</th>
    <th>year</th>
    <th>weekofyear</th>
    <th>total_cases</th>
  </tr>
</thead>
<tbody>
  <tr>
    <th>sj</th>
    <td>2008</td>
    <td>18</td>
    <td>5</td>
  </tr>
  <tr>
    <th>sj</th>
    <td>2008</td>
    <td>19</td>
    <td>5</td>
  </tr>
  <tr>
    <th>sj</th>
    <td>2008</td>
    <td>20</td>
    <td>5</td>
  </tr>
  <tr>
    <th>sj</th>
    <td>2008</td>
    <td>21</td>
    <td>5</td>
  </tr>
  <tr>
    <th>sj</th>
    <td>2008</td>
    <td>22</td>
    <td>5</td>
  </tr>
  <tr>
    <th>...</th>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <th>iq</th>
    <td>2013</td>
    <td>22</td>
    <td>3</td>
  </tr>
  <tr>
    <th>iq</th>
    <td>2013</td>
    <td>23</td>
    <td>3</td>
  </tr>
  <tr>
    <th>iq</th>
    <td>2013</td>
    <td>24</td>
    <td>3</td>
  </tr>
  <tr>
    <th>iq</th>
    <td>2013</td>
    <td>25</td>
    <td>3</td>
  </tr>
  <tr>
    <th>iq</th>
    <td>2013</td>
    <td>26</td>
    <td>3</td>
  </tr>
</tbody>
</table>

</div>

Your `.csv` file that you submit would look like:

  city,year,weekofyear,total_cases
  sj,2008,18,5
  sj,2008,19,5
  sj,2008,20,5
  sj,2008,21,5
  sj,2008,22,5
  ...
  iq,2013,22,3
  iq,2013,23,3
  iq,2013,24,3
  iq,2013,25,3
  iq,2013,26,3

**Keep in mind that you need to submit one csv with predictions for both cities**! Hence the requirement of the `city` column. Results will be parsed on our end and MAE scores will be given for each city's predictions.

## Good luck!

--------

Looking for a great tutorial to get you started? Check out the [benchmark walkthrough](https://www.drivendata.co/blog/dengue-benchmark/) created for this challenge.

Good luck and enjoy this problem! If you have any questions you can always visit the [user forum](http://community.drivendata.org/)!
