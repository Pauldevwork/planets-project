Using Kepler data, I have filtered through it to find potential habitable planets using Node.Js.

I downloaded Nasa's Kepler data from here https://exoplanetarchive.ipac.caltech.edu/docs/data.html  

KOI Table (Cumulative list)
![Screenshot 2024-01-28 003232](https://github.com/Pauldevwork/planets-project/assets/146097501/afd4ab67-03d3-4215-90ca-9f95bf0b61a4)

If this image does not load correctly then visit the link above and download the csv (comma seperated value) file and you will have the data to try this out yourself!

The function below uses the strict equality operator to search for the value 'CONFIRMED', the && (logical and operator) 
to make sure it returns ONLY the specific criteria we are interested in, ie, what is the median temperature (koi_insol 0.36 && 1.11) 
and also the enery they recieve from their parent sun (koi_prad < 1.6).

![Screenshot 2024-01-28 005506](https://github.com/Pauldevwork/planets-project/assets/146097501/3825ee67-063b-45a5-b7a0-0cb473e68a9e)

This parses through 9000+ potential planets in Keplers data, run the code and see how many planets you can find! (i'll give you a hint, I found 8!)



This fs method from csv-parse nmp package creates a 'pipe' between the csv file to our index.js, 
we also tell it that comments are marked with '#' and the colunms are true because we need the column data for our filter to work.

The IF conditional then pushes the data the the empty array 'habitablePlanets'.

![Screenshot 2024-01-28 005644](https://github.com/Pauldevwork/planets-project/assets/146097501/639c6143-53f3-4ee2-82af-0d8f12926fbd)

We then 'end' with our returned data with the planets names, we print out the planets names using a template string .length.
