---
description: >-
  Configure certain aspects of the existing front-ends without the need for a
  recompile.
---

# Settings.json

The settings.json file exists primarily to allow configurable settings that don't require a full rebuild of a frontend - also some visual elements can be controlled by these settings like headings, positions, icons, and colors etc. Some of the configurable settings include:

* Composer settings, like domain, protocol, and auth method.
* Basic App-level visuals; title, meta details, logos, etc.
* Top-level menu listings
* Banner child element organisation and appearance.
* Page routes and titles.
* Bookings - granular conditional settings

The settings.json file can become monolithic but this, for the moment, allows backend devs, or anyone not frontend-familiar with git repo access, the ability to change visuals and other aspects of an app easily.

When approaching an existing frontend first check to see if the change can be made in the settings.json file; it might save some headache.

## Overview

### Composer config

```javascript
{
    ...
    
    "composer": {
        "domain": "",
        "route": "",
        "protocol": "http:",
        "use_domain": true,
        "local_login": false
    }
    
    ...
}
```

The default composer config is setup for simple local development, if you require your app to work in conjunction with a local [ACAEngine instance](../getting-started.md) then the `domain` setting will have to match the corresponding domain listing in the admin panel of the instance \(Backoffice\).

For example:

```javascript
{
    ...
    
    "composer": {
        "domain": "localhost:4200",
        "route": "",
        "protocol": "http:",
        "use_domain": true,
        "local_login": false
    }
    
    ...
}

```

NB: This assumes the app is being served with default settings with the `gulp serve` terminal command - i.e. utilizing port `4200`. A production `settings.json` file will be created from this with modified settings at compile time. These production values overrides will exist within `/config/default.ts`.

### Cosmetics/Supplementary Details

```javascript
{
    ...
    
    "app": {
        "title": "ACA Staff App",
        "name": "Staff App",
        "description": "ACA Projects Staff Application made in Angular",
        "short_name": "ACA",
        "code": "ACA",
        "login": {
            "forgot": false
        },
        "analytics": {
            "enabled": false,
            "tracking_id": "UA-123456789"
        },
        "logo": {
            "type": "img",
            "src": "assets/img/logo.svg",
            "inverse": "assets/img/logo-inverse.svg",
            "background": ""
        },
        "banner": {
            "enabled": true,
            "header": true,
            "home": false,
            "type": "color",
            "full": true,
            "allow_image_on_home": false,
            "src": "assets/img/background-hero.jpg"
        },
        "copyright": "Copyright 2020 ACA Projects",
        
        ...
    }
    
    ...
}
```

In this example basic app-wide details are specified; these include page-wide titles/meta data details, logos, GA code, and toggles for when to show hero banners. All things that can be configured post build.

### Granular Configurations for Sections

This snippet shows the configuration options for room booking on the defauly ACA Staff App.

```javascript
{
    ...
    
    "booking": {
            "min_attendees": 0,
            "external_visitors": false,
            "recurrence": false,
            "max_days_ahead": 180,
            "max_length": 480,
            "default_length": 30,
            "min_length": 30,
            "multi_room": false,
            "title_prefix": "",
            "charge": false,
            "terms": false,
            "old_filters": false,
            "select_room_first": true,
            "privacy": false,
            "control": false,
            "lock_cancel": 0,
            "external_floors": [],
            "return_id": "",
            "fields": [
                {
                    "key": "date",
                    "label": "Date",
                    "icon": {
                        "class": "material-icons",
                        "value": "event"
                    },
                    "simple": true,
                    "description": "",
                    "control_type": "custom",
                    "required": true
                },
                {
                    "key": "start",
                    "label": "Start",
                    "icon": {
                        "class": "material-icons",
                        "value": "access_time"
                    },
                    "refs": [
                        "date"
                    ],
                    "simple": true,
                    "description": "",
                    "control_type": "custom",
                    "required": true
                },
                {
                    "key": "duration",
                    "label": "End",
                    "icon": {
                        "class": "material-icons",
                        "value": "access_time"
                    },
                    "refs": [
                        "date"
                    ],
                    "simple": true,
                    "description": "",
                    "control_type": "custom",
                    "required": true
                }
                
                ...
                
            ],
            "banner": {
                "enabled": true,
                "links": [
                    {
                        "id": "book",
                        "name": "Book Space"
                    },
                    {
                        "id": "book/visitor",
                        "name": "Book Visitor"
                    }
                ]
            }
        }
        
    ...
}
```



