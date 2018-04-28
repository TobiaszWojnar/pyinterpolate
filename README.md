# pyinterpolate
Bunch of spatial interpolation scripts written in numpy and Python

Project pyinterpolate will aggregate GIS spatial interpolation scripts written in numpy and Python 3.6.

## Actual scope of work:

- Fit semivariance
- Simple Kriging function
- Ordinary Kriging function
- Tutorial for calculate_distance function

---

## Done:

#### calculate_distance(points_array)

<b>Python function for calculating a distance between points in n-dimensional space.</b>

* INPUT: points_array - numpy array with points' coordinates where each column indices new dimension 
* OUTPUT: distances - numpy array with euclidean distances between all pairs of points.
IMPORTANT! If input array size has <b>x</b> rows (coordinates) then output array size is x(cols) by x(rows) and each row describes distances between coordinate from row(i) with all rows. The first column in row is a distance between coordinate(i) and coordinate(0), the second row is a distance between coordinate(i) and coordinate(1) and so on.

---

#### calculate_covariogram(points_array, lags, step_size)

<b>Function calculates covariance of points in n-dimensional space.</b>

* INPUT[0]: points_array: numpy array of points and values (especially DEM) where points_array[0] = array([point_x, point_y, ..., point_n, value])
* INPUT[1]: lags: array of lags between points
* INPUT[2]: step_size: distance which should be included in the gamma parameter which enhances range of interest
* OUTPUT: covariance: numpy array of pair of lag and covariance values where covariance[0] = array([lag(i), covariance for lag(i)])

---

#### calculate_semivariogram(points_array, lags, step_size)

<b>Function calculates semivariance of points in n-dimensional space.</b>

* INPUT[0]: points_array: numpy array of points and values (especially DEM) where points_array[0] = array([point_x, point_y, ..., point_n, value])
* INPUT[1]: lags: array of lags between points
* INPUT[2]: step_size: distance which should be included in the gamma parameter which enhances range of interest
* OUTPUT: semivariance: numpy array of pair of lag and semivariance values where semivariance[0] = array([lag(i), semivariance for lag(i)])

-----

### class TheoreticalSemivariogram
Class for calculating theoretical semivariogram. Class takes two parameters during initialization:
* INPUT[0]: points_array - analysed points where the last column represents values, typically DEM
* INPUT[1]: empirical_semivariance - semivariance where first row of array represents lags and the second row represents semivariance's values for given lag

####Available methods:
#### fit_semivariance(model_type, number_of_ranges=200)
* INPUT[0]: model_type: 'exponential', 'gaussian', 'linear', 'spherical'
* INPUT[1]: number_of_ranges: deafult = 200. Used to create an array of equidistant ranges between minimal range of empirical semivariance and maximum range of empirical semivariance.
* OUTPUT: Theoretical model of semivariance (values only)
        
####Static methods:
* spherical_model(distance, nugget, sill, semivar_range)
* gaussian_model(distance, nugget, sill, semivar_range)
* exponential_model(distance, nugget, sill, semivar_range)
* linear_model(distance, nugget, sill, semivar_range)
where:
#### _model(distance, nugget, sill, semivar_range):
* INPUT[0]: distance: array of ranges from empirical semivariance
* INPUT[1]: nugget: scalar
* INPUT[2]: sill: scalar
* INPUT[3]: semivar_range: scalar, optimal range calculated by fit_semivariance method 
* OUTPUT: an array of modelled values for given range. Values are calculated based on the chosen model.

-----

If you have any comments related to the repo feel free to contact me: s.molinski@datalions.eu
