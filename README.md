# MLSoc Website

## Overview
This is the web client for the Imperial College Union Machine Learning Society. It consists of
a static part and a templated part.

It is planned to add interactive demos of past projects.

## Notes for Outreach
The events on the facebook page should always contain the following fields:

* A short title
* A short to medium length description
* A start date and time

It is recommended to add (if available)

* A ticket url (e.g. to the union website)

## Notes for maintainers

### Folder structure
The web server requires the following folder structure (run the server in the root folder
of this structure):

```
  * html_static
    * sponsors
      | Images with the logos of our sponsors
      | NOTE: This folder may ONLY contain image files (e.g. svg, png, ...)
    | Any other static html/css/images/etc.
  * html_templates
    | index.html
  | config.json
```

### Server config
The config file (`config.json`) has the following structure:

```
  {
    "port": ":80",
    "cacheRefreshRate": 3600, (in seconds)
    "printRenderErrors": false,
    "eventsPageId": "fb-page-id",
    "eventsAuthToken": "fb-access-token"
  }
```

The facebook page id can be found in the page settings (you need to be the page owner
to see it there). For generating the permanent access token see [this StackOverflow question](https://stackoverflow.com/questions/17197970/facebook-permanent-page-access-token).

### Templates
All go html templates provided have access to the following data:

```
  struct{
    EventList []events.Event
    EventListSummary []events.Event
    Sponsors []string
  }

  type events.Event struct {
    Picture events.EventPicture
    Title string
    Description string
    StartTime string
    Tickets string
    FacebookId string
  }
  type events.EventPicture struct {
    Source string
    OffsetX int
    OffsetY int
  }
```
