# node-red-contrib-ontime4ibm

![Version: 0.0.5](https://img.shields.io/badge/Version-0.0.5-green.svg)


## Overview

This collection of Node-RED nodes is for OnTime Group Calendar on domino server.

## Description

This package is created by modifying the http request Node.
This package is support to OnTime Group Calendar API on domino server.
It is possible to access easy to OnTime Group Calendar by use by the node that is included in this package.


## Node

OnTime uses the Token API to obtain the Token.
It is necessary to request operation by using that Token.
The nodes of this package stores Token in **msg.ontime.parameters**.
If necessary, obtain or update the Token.
Users do not need to manage Token.


### Token

- token
  - This node requires that the user is authenticated and is used to obtain an OnTime Group Calendar token for use in subsequent requests to the apihttp endpoint.


### Core

- core login
  - Used to verify the token.

- core logout
  - Tell the API that we're logging out. Not critical, more as good behavior and for logging.

- core version
  - Return some version information of API and running server.

- core usersall
  - List of all users and their information.

- core usersinfo
  - Information of specific users.

- core calendars
  - Alle calendar entries for specific users for a given time range.


### Extended

- extended
  - Set the operation and parameters in this node ahead.
  - This node automatically sets ApplID, ApplVer, APIVer, CustomID, Token.

#### Example: FreeRooms: Search for available rooms

![Screenshot](https://github.com/chemp7/node-red-contrib-ontime4ibm/blob/master/example/example01_node-red_flow.PNG)
[Flow](https://github.com/chemp7/node-red-contrib-ontime4ibm/blob/master/example/example01_image.json)

    msg.payload = {
      FreeRooms: {
        StartDT: "2017-12-06T18:00:00Z", 
        EndDT: "2017-12-06T19:00:00Z", 
        Site: "Tokyo", 
        Capacity: 4
      }
    };

- **Note**: All dates shouldbeencodedas stringsin ISO8601 format usingthe UTC timezone. {YYYY}-{MM}-{dd}T{HH}:{mm}:{ss}Z


## Install

Run the following command in the root directory of your Node-RED install.

        npm install node-red-contrib-ontime4ibm


## Licence

Apache License Version 2.0

This software includes the work that is distributed in the Apache License 2.0


## Author

[Takeshi Yoshida](https://github.com/chemp7)


## Releace

2017/12/25 v0.0.5 Specification change
- **Attention**: The output destination of the response from the OnTime API has been changed from `msg.payload` to `msg.ontime.response`.
  - If you were using version 0.0.4 or earlier, update the node config.
  - If you need to include the response in `msg.payload`, please check the checkbox of "Include the response in msg.payload".
- The key name was changed from `msg.OGCParameters` to `msg.ontime.parameters`.
- Added `msg.ontime.response`: This is the response from the OnTime API.
- Added `msg.ontime.request`: This is the content required for the OnTime API. However, it is the state before encoding Unicode.
- Added `msg.ontime.requestEncoded`: This is the content actually requested by the OnTime API after encoding Unicode.
- Deleted `msg.headers` and `msg.statusCode` from output `msg`.

2017/12/02 v0.0.4 hotfix

2017/11/22 v0.0.3 hotfix

2017/11/22 v0.0.2 fix

2017/05/07 v0.0.1 Initial
