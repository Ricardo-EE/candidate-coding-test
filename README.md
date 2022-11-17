# Candidate Technical Test

## Scenario
You are an owner of an industrial facility in the UK, and have a plant or factory that produces emissions out of a
chimney into the atmosphere.
You are obliged by law to record what gases or particulates those are and report these to the authorities.  This is so
we can get a picture of how much pollution is emitted in different places in the country and by what facilities.
This is required for UK government purposes.

Ricardo has a contract for gathering this information across the UK and we have a simple portal where people can log in
and report that their facility has produced these emissions today.

## Docker
This project can be automatically started as a Docker Container, just run: `docker-compose up -d` and visit the URL:
http://localhost:8080.  If you prefer, you can also run via Symfony Web Server, make sure you set-up your own database.

See `docker-compose.yaml` and `Dockerfile` for configuration for MariaDB database

## Requirement
- Generate Doctrine Entities that reflect the most appropriate schema to store the data (using normalisation), with the
aim to easily generate aggregated reports, see `Pollutant Data` section.
- Use Doctrine migrations to build the database schema
- Processing Pollutant Data
  - **Either**; Build a `Symfony Form` for submitting dummy air pollution data,
    see `Example of Pollutants and Measurements HTML form elements`
    - NOTE: You don't have to use the whole dataset.
  - **Or**; Process a file upload using a `Symfony Form` using the supplied `Pollutant Data` file `files/measurements.xlsx`.
- Symfony Controller to process the submitted data
- Use Doctrine to save the data into the MariaDB database detailed in the `docker-compose.yaml` file.
- Produce simple output to get the aggregated total `Measurement` by `Region Name` and `Pollutant`.

### Expectations
**Mandatory**
- SOLID and KISS Principles
- Clean readable code
- Security
- Data Validation
- PHP Coding Standards, Linting (update README.md on how to run)
- PHP Strict Types - must use >= PHP 8.0
- Guard against SQL injection attacks
- Unit Tests (update README.md on how to run)

**Nice to have**
- Functional tests
- Use WebPack and implement Bootstrap: https://getbootstrap.com/

### Bonus - not expected
Use the API https://postcodes.io/postcodes `Bulk Reverse Geocoding` and POST `Longitude` and `Latitude` from the
supplied `Pollutant Data` to retrieve all relevant `admin_county` from API.  Use this instead of the `Region Name`
supplied in the source `Pollutant Data` section detailed below.

### Super Bonus - not expected
Implement ClamAV and virus check the uploaded `Excel` data file - if you choose this route.

Uncomment the ClamAV configurations in the `docker-compose.yaml` file.

**Hint**: Use `fsockopen($hostname, $port)` and a `Drupal` example may help you.  
See `.env` for ClamAV environment variables.

### Pollutant Data
As stated in the requirements, you can either build a Symfony Form with all the data supplied as `input` fields in a
`Symfony Form` or use a `Symfony Form` to upload the supplied `Excel` data file and process it.

- Data File: `files/measurements.xlsx`

Data submitted via an HTML form will be as follows:

**Data is hourly**
- Company (string) - Max allowed length 100
- Region Name (string) - Max allowed length 100
- Site Name (string) - Max allowed length 100
- Latitude (float)
- Longitude (float)
- List of Pollutants (string) and Measurements (float)
- Date (string)
- Time (string)

#### Example of Pollutants and Measurements HTML form elements:
```html
<input type="text" name="measurement[pollutant][NO2]" value="2.00">
<input type="text" name="measurement[pollutant][SO2]" value="3.00">
<input type="text" name="measurement[pollutant][PM25]" value="8.00">
<input type="text" name="measurement[pollutant][PM10]" value="11.00">
<input type="text" name="measurement[pollutant][O3]" value="66.00">
```

Copyright © 2022 Ricardo AEA Ltd