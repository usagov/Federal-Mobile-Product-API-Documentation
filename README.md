# Federal Mobile Product API Documentation

## On This Page

*   [About the API](#about-the-api)
*   [Accessing the API](#accessing-the-api)
*   [Terms of Service](#terms-of-service)

## About the API

The [Federal Mobile Apps Directory](http://www.usa.gov/mobileapps.shtml) and [GobiernoUSA.gov Aplicaciones (apps) móviles](http://www.usa.gov/gobiernousa/conectese-gobierno/apps.moviles.shtml) feature mobile apps and websites from government agencies on a variety of platforms in English and Spanish.

The Federal Mobile Product API can be used to retrieve information about all of the apps and mobile sites in the directories.

If you are using the Federal Mobile Product API and have feedback or want to tell us about your product, please [e-mail us](mailto:usagov-developers@gsa.gov).

## Accessing the API

Our Federal Mobile Product API is accessible via HTTP GET requests and does not require a login or API key to use.

The base URL for the API is http://apps.usa.gov/apps-gallery/api/. Append the API call you'd like to make to this URL.

There are 4 URLs available to query against.

*   Return a list of all public registrations.

    [http://apps.usa.gov/apps-gallery/api/registrations.json](http://apps.usa.gov/apps-gallery/api/registrations.json)

*   Return single public registration by appending it's system Id.

    http://apps.usa.gov/apps-gallery/api/registrations/{ID}.json

*   Return a list of all galleries and their public registrations

    [http://apps.usa.gov/apps-gallery/api/galleries.json](http://apps.usa.gov/apps-gallery/api/galleries.json)
    

*   Return a gallery and it's public registrations by appending it's system Id.

    http://apps.usa.gov/apps-gallery/api/galleries/{ID}.json
    

### Query Examples

*   Search by one or more properties (wildcards supported):

    [http://apps.usa.gov/apps-gallery/api/registrations.json?Name=*Department*](http://apps.usa.gov/apps-gallery/api/registrations.json?Name=*Department*)
    

*   Search by property using 'OR' by using the same parameter multiple times:

    [http://apps.usa.gov/apps-gallery/api/registrations.json?Name=D*&Name=S*](http://apps.usa.gov/apps-gallery/api/registrations.json?Name=D*&Name=S*)
    

*   Search by property of subdocument:

    [http://apps.usa.gov/apps-gallery/api/registrations.json?Version_Details.Platform=iOS](http://apps.usa.gov/apps-gallery/api/registrations.json?Version_Details.Platform=iOS)
    

*   Sort by a property (DESC) and then by another property (ASC):

    [http://apps.usa.gov/apps-gallery/api/registrations.json?Name=*L*&sort=-Version_Details.Platform&sort=Name](http://apps.usa.gov/apps-gallery/api/registrations.json?Name=*L*&sort=-Version_Details.Platform&sort=Name)
    

*   Search by property using 'LESS THAN' and 'GREATER THAN':

    [http://apps.usa.gov/apps-gallery/api/registrations.json?Name=<B&Name=>P](http://apps.usa.gov/apps-gallery/api/registrations.json?Name=<B&Name=>P)
    

*   Only include the selected fields:

    [http://apps.usa.gov/apps-gallery/api/registrations.json?Name=D*&select=Name&select=Short_Description](http://apps.usa.gov/apps-gallery/api/registrations.json?Name=D*&select=Name&select=Short_Description)
    

*   Include all fields except the select fields (NOTE: You can't mix includes/excludes. All must be without '-', or all with '-'):

    [http://apps.usa.gov/apps-gallery/api/registrations.json?Name=D*&select=-Meta_Details&select=-Version_Details](http://apps.usa.gov/apps-gallery/api/registrations.json?Name=D*&select=-Meta_Details&select=-Version_Details)
    

*   Return the first 10 records:

    [http://apps.usa.gov/apps-gallery/api/registrations.json?Name=*D*&limit=10](http://apps.usa.gov/apps-gallery/api/registrations.json?Name=*D*&limit=10)
    

*   Return the first 10 records and start at record 5:

    [http://apps.usa.gov/apps-gallery/api/registrations.json?Name=*D*&limit=10&offset=5](http://apps.usa.gov/apps-gallery/api/registrations.json?Name=*D*&limit=10&offset=5)
    

### Error Handling

*   HTTP Code 500 = internal server error
*   HTTP Code 200 = results found
*   HTTP Code 404 = query error

### JSONP

*   JSONP callback functions are supported via the _callback parameter

    [http://apps.usa.gov/apps-gallery/api/registrations.json?Name=D*&_callback=MY_FUNC](http://apps.usa.gov/apps-gallery/api/registrations.json?Name=D*&_callback=MY_FUNC)
    

### API Data Model

The following fields are associated with mobile apps. Please note that not every record has data in every field, and the API will only return completed fields.

*   **Id** - Unique Sytem Id of the app.
*   **Name** – The name of the app.
*   **Organization** – The agency or organization for the app.
*   **Friendly_URL** – The URL to the app on the USA.gov or GobiernoUSA.gov App Gallery.
*   **Short_Description** – A short description of the app.
*   **Long_Description** – A long description of the app. Please note that the long description may include HTML coding.
*   **Language** – Whether the app is in English or Spanish.
*   **Icon** – The path to the icon for the app.
*   **Agency** - Agency associated with the app as an array.
*   **Version_Details** - List of version avaiable for the app as an array.

Additionally, each Version Detail section includes following sub-data elements.

*   **Version_Number** - This version's number,
*   **Published** - The date this version of the app was published.
*   **Description** - Description of this version, should be similar to the registration's long description,
*   **Store_Url** -The URL to download or access the app.
*   **Whats_New** - Description of changes or features distinct to this version.
*   **Platform** - Operating System this version is available for.
*   **Device** - List of device types this version is available for as an array.
*   **Rating** - Average rating of this version.
*   **Rating_Count** - Number of ratings given.
*   **Screenshot** - List of url paths to screenshots of the app as an array.
*   **Video** - List of url paths to videos of the app as an array.
*   **Language** - Whether this version is in English or Spanish.

### Results

All results are in json format.

No Results

    {
            "metadata": {
                "uri":    "http://apps.usa.gov/apps-gallery/api/registrations.json?Name=NotFound",
                "count":  0,
                "offset": null
            },
            "results": []
    }

Good Results

    {
            "metadata": {
                "uri":    "http://apps.usa.gov/apps-gallery/api/registrations.json?limit=3",
                "count":  3,
                "limit":  3,
                "offset": 1
            },
            "results": [ {},{},{} ]
    }

JSONP Results

    fname({
            "metadata": {
                "uri":    "http://apps.usa.gov/apps-gallery/api/registrations.json?limit=3&_callback=fname",
                "count":  3,
                "limit":  3,
                "offset": 1
            },
            "results": [ {},{},{} ]
    });

## Terms of Service

By using this data, you agree to the [Terms of Service](/About/developer-resources/terms-of-service.shtml).