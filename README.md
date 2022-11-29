# Candidate Technical Test

## Scenario
You are an owner of an industrial facility in the UK, and have a plant or factory that produces emissions out of a
chimney into the atmosphere.
You are obliged by law to record what gases or particulates those are and report these to the authorities.  This is so
we can get a picture of how much pollution is emitted in different places in the country and by what facilities.
This is required for UK government purposes.

Ricardo has a contract for gathering this information across the UK and we have a simple portal where people can log in
and report that their facility has produced these emissions today.

## Symfony Framework
This project has already been set-up for you, including a MariaDB database and appropriate doctrine configuration, as
well as all the necessary `composer` dependencies required to complete the task.

## Docker
This project can be automatically started as a Docker Container, just run: `docker-compose up -d` and visit the URL:
http://localhost:8080.  It is expected that your submission will work with the supplied Docker set-up in this project.

See `docker-compose.yaml` and `Dockerfile` for configuration for MariaDB database

## Requirement
- Generate Doctrine Entities that reflect the most appropriate schema to store the data (using normalisation), with the
aim to easily generate aggregated reports, see `Pollutant Data` section.
- Use Doctrine migrations to build the database schema
- Processing Pollutant Data
  - **Either**; Process a file upload using a `Symfony Form` using the supplied `Pollutant Data`
file `files/measurements.xlsx`
    - **IMPORTANT**: Data uploads should be stored into the directory `data/uploads/`
  - **Or**; Create a `Symfony Command` to process the file.
- Use Doctrine to save the data into the MariaDB database detailed in the `docker-compose.yaml` file.
- Produce simple output to get the aggregated total `Measurement` by `Region Name` and `Pollutant`.  CSV format is fine.

## Expectations
**Mandatory**
- SOLID and KISS Principles
- Use PHP Strict Types
- Clean readable code
- PHP Coding Standards
  - These tools are installed via `composer.json` please make sure you use them.

## Pollutant Data
As stated in the requirements, you can either;
- Use a `Symfony Form` to upload the supplied `Excel` data file
  - Data uploads should be stored in the directory `data/uploads/`
- Or, use `Symfony Command` to process the supplied `Excel` data file

**If you'd prefer, you can convert the supplied spreadsheet to a CSV file to avoid using a Spreadsheet processor.**

**Data File**: `files/measurements.xlsx`

**Data is hourly**
- Region Name (string) - Max allowed length 100
- Site Name (string) - Max allowed length 100
- Pollutant (string)
- Measurement (float)
- Date (string)
- Time (string)

## Submitting Your Solution
After you have completed your solution, please push to your own GitHub repository and provide us with a link to
review your submission.

Please provide any additional instructions if there are any special set-up requirements.

Copyright © 2022 Ricardo AEA Ltd
