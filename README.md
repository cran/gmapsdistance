gmapsdistance
=======
[![R-CMD-check](https://github.com/jlacko/gmapsdistance/workflows/R-CMD-check/badge.svg)](https://github.com/jlacko/gmapsdistance/actions)
![Downloads-monthly](https://cranlogs.r-pkg.org/badges/gmapsdistance?color=brightgreen)
![Downloads-total](https://cranlogs.r-pkg.org/badges/grand-total/gmapsdistance?color=brightgreen)
![License](https://img.shields.io/badge/license-GPL--3-brightgreen.svg?style=flat)
[![CRAN_Status_Badge](https://www.r-pkg.org/badges/version/gmapsdistance)](https://cran.r-project.org/package=gmapsdistance)
[![CRAN-checks](https://badges.cranchecks.info/summary/gmapsdistance.svg)](https://cran.r-project.org/web/checks/check_results_gmapsdistance.html)
[![Codecov test coverage](https://codecov.io/gh/jlacko/gmapsdistance/branch/master/graph/badge.svg)](https://app.codecov.io/gh/jlacko/gmapsdistance?branch=master)

# Interface Between R and Google Maps

The function `gmapsdistance` uses the [Google Maps Distance Matrix API](https://developers.google.com/maps/documentation/distance-matrix/overview?hl=en) to compute the distance(s) and time(s) between two points or two vectors of points using one of the four defined modes of transportation: `bicycling`, `walking`, `driving`, `transit`. The distance is returned in meters and the time in seconds. 

An [API key](https://developers.google.com/maps/documentation/distance-matrix/get-api-key#key) is necessary to perform the query. Google maps must be able to find both the origin and the destination in order for the function to run. 

While the R package is open source the Distance Matrix API itself is a commercial service, requiring registration in all cases. 

A free tier is provided - $200 monthly credit. This is enough for 40,000 [Distance Matrix](https://developers.google.com/maps/documentation/distance-matrix/usage-and-billing?w#distance-matrix) calls or 20,000 [Distance Matrix Advanced](https://developers.google.com/maps/documentation/distance-matrix/usage-and-billing?w#distance-matrix-advanced) calls – more than sufficient for most R package users.

Also note that using the API is subject to [Google Maps Platform Terms of Service](https://cloud.google.com/maps-platform/terms).


## Installation

```r
# CRAN install / stable version 
install.packages("gmapsdistance")

# Github installation / current dev version
remotes::install_github("jlacko/gmapsdistance")
```

## Examples of use
In this example we will compute the driving distance between Washington DC, and New York City. The code returns the `Time`, the `Distance` and the `Status` of the query (`OK` if it was successful).

``` r
results <- gmapsdistance(origin = "Washington DC", 
                        destination = "New York City NY", 
                        mode = "driving",
                        key = Sys.getenv("GOOGLE_API_KEY")) # your actual API key comes here...
results
# $Time
# [1] 14523
# 
# $Distance
# [1] 367656
# 
# $Status
# [1] "OK"
```

This example computes distance matrix between two vectors of cities at a specific departure time. The code displays resulting distance matrices using time (in seconds) and travel distance (in meters) as metrics.

``` r
results <- gmapsdistance(origin = c("Washington DC", "New York NY", "Seattle WA", "Miami FL"), 
                         destination = c("Washington DC", "New York NY", "Seattle WA", "Miami FL"), 
                         mode = "bicycling",
                         dep_date = "2022-05-31", # provided as string in ISO 8601 format
                         dep_time = "12:00:00", # provided as string in HH:MM:SS format
                         key = Sys.getenv("GOOGLE_API_KEY")) # your actual API key comes here...
                        
results$Time
#               Washington DC New York NY Seattle WA Miami FL
# Washington DC             0       76753     893416   353377
# New York NY           76537           0     917724   429533
# Seattle WA           890818      922255          0  1045150
# Miami FL             350851      427721    1048150        0

results$Distance
#               Washington DC New York NY Seattle WA Miami FL
# Washington DC             0      388695    4762468  1919628
# New York NY          384224           0    5028313  2303263
# Seattle WA          4754835     5049618          0  5638340
# Miami FL            1909272     2298117    5651681        0
```
## Usage limits
There are a set of limits to the  number of calls that can be done. These limits are established by the [Google Maps Distance Matrix API](https://developers.google.com/maps/documentation/distance-matrix/usage-and-billing)

## License
[GNU General Public License v3.0](https://github.com/jlacko/gmapsdistance/blob/master/LICENSE.md)

## How to contribute
We encourage any kind of suggestions to improve the quality of this code. You can submit pull requests indicating clearly what is the purpose of the change and why we should accept such pull request. Although not necessary, we encourage you to verify that your suggestions are in accordance with the general guidelines established in the CRAN repository by running the R CMD check command.

## Code of conduct
Please see the file [CODE_OF_CONDUCT.md](https://github.com/jlacko/gmapsdistance/blob/master/CODE_OF_CONDUCT.md) for the Code of Conduct for the Contributor Covenant Code of Conduct. 


## Authors
This code was developed originally by [Rodrigo Azuero](http://rodrigoazuero.com/) and [David Zarruk](http://www.davidzarruk.com/).

It is currently maintained by [Jindra Lacko](mailto:jindra.lacko@gmail.com).

[AUTHORS.md](https://github.com/jlacko/gmapsdistance/blob/master/AUTHORS.md) have a list of everyone who have contributed to gmapsdistance.

## Where has gmapsdistance be used/mentioned.
We like to keep track of the projects where gmapsdistance has been used. This will help us identify how to better improve the code. Let us know if you use gmapsdistance! Below you will find links to some of the projects and some of the references to gmapsdistance that we have found. 

1. Proximity to pediatric cardiac specialty care for adolescents with congenital heart defects. [Link to article](https://doi.org/10.1002/bdr2.1129). 

2. Measuring Accessibility to Rail Transit Stations in Scarborough: Subway vs. LRT. [Link to article](https://www.torontomu.ca/content/dam/tedrogersschool/documents/Measuring%20accessibility%20to%20rail%20transit%20stations%20in%20Scarborough-final.pdf)

3. Social Data Science Course. University of Copenhagen. Department of Economics. [Link](https://sebastianbarfort.github.io/sds_summer/slides/gathering.pdf)

4. R-bloggers. The collaborative innovation landscape in data science. [Link](https://www.r-bloggers.com/2016/07/the-collaborative-innovation-landscape-in-data-science/)

5. RPubs. [Link](https://rpubs.com/mattdray/gmapsdistance-test) 

6. Identifying Partnership Opportunities at Air Force Installations: A Geographic Information Systems Approach [Link](https://scholar.afit.edu/etd/810/) 

7. DataWookie. Review of gmapsdistance. [Link](https://datawookie.dev/blog/2017/08/route-asymmetry-in-google-maps/)

8. The Role of Telehealth in Promoting Equitable Abortion Access in the United States: Spatial Analysis [Link to article](https://publichealth.jmir.org/2023/1/e45671)

9. The relationship between living in urban and rural areas of Scotland and children’s physical activity and sedentary levels: a country-wide cross-sectional analysis [Link to article](https://doi.org/10.1186/s12889-020-8311-y)

10. E-trikes for urban delivery: An empirical mixed-fleet simulation approach to assess city logistics sustainability [Link to article](https://doi.org/10.1016/j.scs.2023.104641)
