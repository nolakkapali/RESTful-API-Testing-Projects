# World Population API Testing <br>
A dummy API will be developed to manage world population data,allowing users to perform Create,View,Update and Delete operations.Comprehensive API testing will be performed to validate the functionality of these operations.<br>

Project Link: [World Population API Postman](https://www.postman.com/nolakkapali/nolak-s-workspace/collection/5v8floy/world-population?action=share&creator=30401768 'Visit Postman')

### 1) Develope Dummy API:

<ol>

#### Step-1: Install NodeJS<br>
Download Link: https://nodejs.org/en/download<br>
#### Step-2: Open cmd/terminal<br>
Check Node and npm version:<br>
```node --version```<br>
```npm --version```<br>
#### Step-3: Install Json server<br>
```npm install -g json-server```<br>
#### Step-4: Download world population JSON file<br>
Sample JSON file:
```{
    "world-population": [
    {
      "Country Name": "Arab World",
      "Country Code": "ARB",
      "Year": "1960",
      "Value": "263880685769",
      "id": "5117"
    },
    {
      "Country Name": "Arab World",
      "Country Code": "ARB",
      "Year": "1961",
      "Value": "98882541.4",
      "id": "5a0b"
    },
    ....
  ]
}
```
#### Step-5: Open the command prompt where the Json file is present:
Type the below command in cmd/terminal:
<br>
```json-server world-population.json```<br> 

![Image](https://github.com/user-attachments/assets/6645808e-c5fc-460e-8b77-885b793b5000) <br>
#### Generated URI:  http://localhost:3000/world-population<br>
This REST API shows all the world population data available in the JSON file <br>

![Image](https://github.com/user-attachments/assets/9040d956-b7d5-48ab-84ba-250341397946)<br>
***Created API should be running till the cmd/terminal is closed<br>***
</ol>

### 2) Create Postman Collections:
<ol>

<b>Step-1:</b> Design and create API testcases<br>
<b>Step-2:</b> Go to Postman<br>
<b>Step-3:</b> Create Collections, folders, http requests, variables based on test cases<br><br>
<b>Sample Requests:</b>
<table>
<th>Functionality</th>
<th>HTTP Methods</th>
<th>URIs</th>
<tr>
<td>View the world population based on country name</td>
<td>GET Request</td>
<td> http://localhost:3000/world-population?Country Name=Australia</td>
</tr>

<tr>
<td>Adding a new country population data</td>
<td> POST Request</td>
<td> http://localhost:3000/world-population</td>
</tr>

<tr>
<td>Update a country population data</td>
<td> PUT Request</td>
<td> http://localhost:3000/world-population/:id</td>
</tr>

<tr>
<td>Update only year information of a single country</td>
<td> PATCH Request</td>
<td> http://localhost:3000/world-population/:id</td>
</tr>

<tr>
<td>Delete a single country population data</td>
<td> DELETE Request</td>
<td> http://localhost:3000/world-population/:id</td>
</tr>
</table>
</ol>

### 3) Run Postman Collections:

<ol>

#### 1) Postman collection can be run in the postman runner

<ol>
<b>Step-1:</b> Import the collection file and run the collection in postman runner<br>
</ol>

#### 2) Postman collection can be run in newman
<ol>

#### Step-1: Open the cmd/terminal
Type the command in cmd:<br>
Install the htmlextra package:<br>
```npm install -g newman-reporter-htmlextra```
<br>Generate Report:<br>
```newman run "World Population.postman_collection.json" -d world-population.json -r htmlextra```
</ol>
</ol>
