# Spotify Web API
Spotify is a music player web application.In this project, multiple spotify API endpoints are tested to validate the functionality of the web application.
<br> 

Project Link: [Spotify Web API Postman](https://www.postman.com/nolakkapali/nolak-s-workspace/collection/xivurzl/spotify-api?action=share&creator=30401768 'Visit Postman')

### Step-1) Visit [Spotify For Developers](https://developer.spotify.com/)<br>
<ul>
<b>Step-1:</b> Log in and Go to Dashboard<br>
<b>Step-2:</b> Create an app and select Web API in the form<br>
<b>Step-3:</b> Tap the app<br>
<b>Step-4:</b> Go to settings<br>
<b>Step-5:</b> Save below link in Redirect URIs

`https://oauth.pstmn.io/v1/browser-callback` <br>
<b>Step-6:</b> Copy Client ID and Client Secret</ul>

### Step-2) OAuth 2.0 Authorization:
<ol>
<b>Step-1:</b> Create Spotify collection<br> 
<b>Step-2:</b> Go to authorization tab and select 

`Auth Type : OAuth 2.0`<br> 
<b>Step-3:</b> Paste CallBack URL from Postman OAuth 2.0 documentation<br> 
<b>Step-4:</b> Create Spotify environment<br> 
<b>Step-5:</b> Turned the Client ID and Client Secret as Environment Variable Under Spotify environment<br> 
<b>Step-6:</b> Paste the variables beside their respective name fields<br> 
<b>Step-7:</b> Go to the Spotify developers website<br> 
<b>Step-8:</b> Visit Documentation->Web APIs-> Concepts<br> 
<b>Step-9:</b> For our OAuth 2.0 Grant type is Authorization Code and the authorization Code flow is given below:<br> 
imagee<br> 
<b>Step-10:</b> Fill up Access token, Auth URL, Scope based on the authorization guide in the Spotify Documentation<br> 
<b>Step-11:</b> Click Get New Access Token<br> 
<b>Step-12:</b> Access token is generated then Click Use token </ol>

### Step-3) Design Spotify Collection in Postman
<ol><b>Step-1:</b> Go to the Documentation->Web APIs-> References<br>
<b>Step-2:</b> Create Album,Playlist,Artists,Search,Tracks,Genre,Player folders and select API endpoints from Spotify References and create http requests on those folders<br>
<b>Step-3:</b> Create environment variables based on those http requests<br>
<b>Step-4:</b> Add test assertions in collection,folder and http requests level to validate status name,code,JSON schema etc.<br><br>
<b>Sample Requests:</b><br>
<table>
<th>Folders</th>
<th>Requests</th>
<th>HTTP Methods</th>
<th>URIs</th>
<tr>
<td rowspan ="2">Album</td>
<td>View Single Album</td>
<td>GET Request</td>
<td>https://api.spotify.com/v1/albums/:id?market=ES</td>
</tr>

<tr>
<td>Save Albums for Current User</td>
<td> PUT Request</td>
<td>https://api.spotify.com/v1/me/albums?ids={{album_ids}}</td>
</tr>

<tr>
<td rowspan ="1">Users</td>
<td>Unfollow Playlist</td>
<td> PUT Request</td>
<td> https://api.spotify.com/v1/playlists/:playlist_id/followers</td>
</tr>

<tr>
<td rowspan ="2">Playlist</td>
<td>Create Playlist</td>
<td> Post Request</td>
<td>https://api.spotify.com/v1/users/:user_id/playlists</td>
</tr>

<tr>
<td>Updating Items in Playlist</td>
<td> PUT Request</td>
<td>https://api.spotify.com/v1/playlists/:playlist_id/tracks</td>
</tr>

<tr>
<td rowspan ="1">Artists</td>
<td>View Single Artist</td>
<td>GET Request</td>
<td>https://api.spotify.com/v1/artists/:id</td>
</tr>
<tr>
<tr>
<td rowspan ="1">Player</td>
<td>View Playback State</td>
<td>GET Request</td>
<td>https://api.spotify.com/v1/me/player?market=CA</td>
</tr>
<tr>
<td rowspan ="2">Tracks</td>
<td>View Track</td>
<td>GET Request</td>
<td>https://api.spotify.com/v1/tracks/:id?ES=CA</td>
</tr>
<tr>
<td>Save Tracks for Current User</td>
<td>PUT Request</td>
<td>https://api.spotify.com/v1/me/tracks</td>
</tr>
</table><br>
<b>Sample test assertions:</b><br><i>Validation of Status Code and Status Name:</i> <br>

```
// Get the status code from the response
let stat_code = pm.response.code;

// Check for different status codes and their corresponding names

  pm.test("Status Code is 201", () => {
    pm.response.to.have.status(201);
      console.log("Resource was successfully created");
    });
  pm.test("Status Name is Created",() => {
    pm.response.to.have.status("Created");
    }); 

```
<br>
<i>Validation of JSON Schema:</i>

```let device_schema={
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Generated schema for Root",
  "type": "object",
  "properties": {
    "devices": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {
            "type": "string"
          },
          "is_active": {
            "type": "boolean"
          },
          "is_private_session": {
            "type": "boolean"
          },
          "is_restricted": {
            "type": "boolean"
          },
          "name": {
            "type": "string"
          },
          "supports_volume": {
            "type": "boolean"
          },
          "type": {
            "type": "string"
          },
          "volume_percent": {
            "type": "number"
          }
        },
        "required": [
          "id",
          "is_active",
          "is_private_session",
          "is_restricted",
          "name",
          "supports_volume",
          "type",
          "volume_percent"
        ]
      }
    }
  },
  "required": [
    "devices"
  ]
}
// JSON Schema validation test
pm.test("Validate JSON Schema",() =>
{
    pm.response.to.have.jsonSchema(device_schema);
    
}
);
```
</li>
</ol>

###  Step-4) Run Spotify Collection 

<ol>

#### 1) Postman collection can be run in the postman runner
<ol>

#### Step-1:
Import the collection and environment file and run the files in postman runner<br>
</ol>

#### 2) Postman collection can be run in the command prompt
<ol> 

#### Step-1: Type in the command prompt:

Generate a report:<br>
`newman run "Spotify API.postman_collection.json" -e "Spotify Environment.postman_environment.json" -r cli`
</ol>

#### 3) Postman collection can be run in newman
<ol>

#### 1. Newman HTML Report<br>
Open the cmd/terminal<br>
Install html reporter:<br>
`npm install -g newman-reporter-html`<br>
Generate html report:<br>
`newman run "Spotify API.postman_collection.json" -e "Spotify Environment.postman_environment.json" -r html`
#### 2. Newman htmlextra report
Install the htmlextra package:<br>
```npm install -g newman-reporter-htmlextra```
<br>Generate htmlextra report:<br>
`newman run "Spotify API.postman_collection.json" -e "Spotify Environment.postman_environment.json" -r htmlextra`
</ol>
</ol>

