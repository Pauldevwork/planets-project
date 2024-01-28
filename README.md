Using Kepler data, I have filtered through it to find potential habitable planets using Node.Js.

I downloaded Nasa's Kepler data from here https://exoplanetarchive.ipac.caltech.edu/docs/data.html  

KOI Table (Cumulative list)
![Screenshot 2024-01-28 003232](https://github.com/Pauldevwork/planets-project/assets/146097501/afd4ab67-03d3-4215-90ca-9f95bf0b61a4)

If this image does not load correctly then visit the link above and download the csv (comma seperated value) file and you will have the data to try this out yourself!

The function below uses the strict equality operator to search for the value 'CONFIRMED', the && (logical and operator) 
to make sure it returns ONLY the specific criteria we are interested in, ie, what is the median temperature (koi_insol 0.36 && 1.11) 
and also the enery they recieve from their parent sun (koi_prad < 1.6).

This parses through 9000+ potential planets in Keplers data, run the code and see how many planets you can find! (i'll give you a hint, I found 8!)

![Screenshot 2024-01-28 005353](https://github.com/Pauldevwork/planets-project/assets/146097501/38f9d4fe-9eea-4dc9-9df0-8e3b8095da27)

function isHabitablePlanet(planet) {
    return planet['koi_disposition'] === 'CONFIRMED'
    && planet['koi_insol'] > 0.36 && planet['koi_insol'] < 1.11
    && planet['koi_prad'] < 1.6;
}

This fs method from csv-parse nmp package creates a 'pipe' between the csv file to our index.js, 
we also tell it that comments are marked with '#' and the colunms are true because we need the column data for our filter to work.

The IF conditional then pushes the data the the empty array 'habitablePlanets'.

fs.createReadStream('kepler_data.csv')
    .pipe(parse({
        comment: '#',
        columns: true,
    }))
    .on('data', (data) => {
        if(isHabitablePlanet(data)) {
            habitablePlanets.push(data);
        }
})
.on('error', (err) => {
    console.log(err);
})

.on('end', () => {
    console.log(habitablePlanets.map((planet) => {
        return planet['kepler_name'];
    }));
    console.log(`${habitablePlanets.length} habitable planets found!`);
});


we then 'end' with our returned data with the planets names, we print out the planets names using a template string .length.
