# Public Preview

This application demonstrates the usage of Preview API. With this API it is possible to have a preview on SmartHub main screen showing what content is available in application. It provides a way for deeplinking to specific parts of application to directly access the desired content.


## How to use the Public Preview application

In order to use Preview follow the procedure:

1. Launch Preview Server (see PreviewServer app)
2. Launch Streaming Server (see StremaingServer app)
3. Install and launch Preview App
4. Add shortcut to Preview bar (go to Apps panel, press and hold **ENTER** button on desired app - menu will appear, choose **Add to Home**)

If a TV can access **Preview Server** and **Streaming Server** user should see the preview tiles on Preview bar on SmartHub home screen. 
When user clicks on desired content the application will be launched and chosen content should start to play.

The application itself is a simple VOD player. Use TV remote controller to choose the movie and control playback.


## Supported platforms

2016 and newer


## Prerequisites

In order for Preview to work user needs to launch a Preview Server providing a JSON file with preview data (see PreviewServer app).  
Preview Server app contains `preview.json` file with data for public preview. It also contains `videos.json` with URLs to video streams that can be played in the application. Replace the resource URLs in mentioned JSON files with the ones fitting your environment. StreamingServer app can be used for serving the example streams.

To use Preview API, embed below script into your `index.html`:

```html
<script type="text/javascript" src="$WEBAPIS/webapis/webapis.js"></script>
```

## Privileges and metadata

In order to use Preview API the following privileges and metadata must be included in `config.xml`:

```xml
<tizen:metadata key="http://samsung.com/tv/metadata/use.preview" value="endpoint_URL=http://yourServer/JSONfile.json"></tizen:metadata>
```

Replace `http://yourServer/JSONfile.json` with address of Preview Server directing to JSON file with preview data.

Disable reloading the application main page when it receives an application control request. This allows your application, if it is already running, to receive the `action_data` information without reloading:

```xml
<tizen:app-control>
    <tizen:src name="index.html" reload="disable"></tizen:src>
    <tizen:operation name="http://samsung.com/appcontrol/operation/eden_resume"></tizen:operation>
</tizen:app-control>
```

The final thing is to put the correct backend server address in application (Preview Server is responsible for this). Find the following line at the beginning of `js/main.js`:  

```javascript
var SERVER_ADDRESS = 'http://192.168.137.1';
```

### File structure

```
PublicPreview/ - PublicPreview sample app root folder
│
├── assets/ - resources used by this app
│   │
│   └── JosefinSans-Light.ttf - font used in application
│
├── css/ - styles used in the application
│   │
│   ├── main.css - styles specific for the application
│   └── style.css - style for application's template
│
├── js/ - scripts used in the application
│   │
│   ├── init.js - script that runs before any other for setup purpose
│   ├── keyhandler.js - module responsible for handling keydown events
│   ├── logger.js - module allowing user to register logger instances
│   ├── main.js - main application script
│   ├── navigation.js - module responsible for handling in-app focus and navigation
│   ├── utils.js - module with useful tools used through application
│   └── videoPlayer.js - module controlling AVPlay player
│
├── CHANGELOG.md - changes for each version of application
├── config.xml - application's configuration file
├── icon.png - application's icon
├── index.html - main document
└── README.md - this file
```

## Other resources

*  **Preview API**  
  https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/preview-api

*  **Public Preview Implementation**  
  https://developer.samsung.com/tv/develop/guides/smart-hub-preview/implementing-public-preview


## Copyright and License

**Copyright 2019 Samsung Electronics, Inc.**

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
