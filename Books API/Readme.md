# Data Driven Testing on Books API
This API allows user to reserve a book.<br> Data driven testing is performed in Books API, allowing users to perform API testing for larger datasets validating functionality of Books API.<br> 

API Available Link: https://simple-books-api.glitch.me<br>
API Documentation Link: [simple-books-api.md](https://github.com/vdespa/introduction-to-postman-course/blob/main/simple-books-api.md)<br>
Project Link: [Books API Postman Link](https://www.postman.com/nolakkapali/nolak-s-workspace/collection/6wqqlxq/books-api-test?action=share&creator=30401768 'Visit Postman')

### Developing Postman Collection
***
<li>Postman API collection should be developed according to the Books API testcases</li>
<li> For data driven testing, all the data parameters are extracted from Book_Data csv file</li>
<li> All the data parameters must be included in the request body of POST/PATCH request as data variables and collection variables need to be generated to store response values</li>
<li>Test assertions are performed on folder and request level to validate the respective operation's functionality</li>
<br>
<i>Sample test assertions for token generation:</i> <br> 

```
//Store Token Value as Collection Variable
let token=pm.response.json();
pm.collectionVariables.set("token",token.accessToken);

//Check Status Code Should be 201
pm.test("Status Code is 201", () => {
    pm.response.to.have.status(201);
});

//Check Status Name Should be "Created"
pm.test("Status Name is Created",() =>
{
pm.response.to.have.status("Created");
});

//Check Response Headers
//check Response(Content-Type) Header Presence 
pm.test("Content-Type header is present", () =>
{
    pm.response.to.have.header("Content-Type");
}
);

//Check Header Value
pm.test("Response Header Has Proper Value", () => {
    pm.expect(pm.response.headers.get("Content-Type")).to.eql("application/json; charset=utf-8");
});
```

### API Endpoints
***

<table>
<th>Requests</th>
<th>Http Methods</th>
<th>Endpoints</th>
<th>API Authentication</th>
<th>Additional Information</th>
<tr>
<td>View API Status</td>
<td>GET</td>
<td>/status</td>
<td>N/A</td>
<td>N/A</td>

</tr>
<tr>
<td>View List of Books</td>
<td>GET</td>
<td>/books</td>
<td>N/A</td>
<td><b>Optional Query Parameter:<br></b> <b>type:</b> fiction or non-fiction<br>
<b>limit:</b> a number between 1 and 20.</td>
</tr>
<tr>
<td>Get a single book</td>
<td>GET</td>
<td>/books/:bookId</td>
<td>N/A</td>
<td>N/A</td>
</tr>
<tr>
<td>Submit an order</td>
<td>POST</td>
<td>/orders</td>
<td>Requires authentication</td>
<td>The request body needs to be in JSON format and include the following properties:<br><b>bookId-</b> Integer - Required<br>
<b>customerName-</b> String - Required</td>
</tr>
<tr>
<td>View all orders</td>
<td>GET</td>
<td>/orders</td>
<td>Requires authentication</td>
<td>N/A</td>
</tr>
<tr>
<td>View an existing order</td>
<td>GET</td>
<td>/orders/:orderId</td>
<td>Requires authentication</td>
<td>N/A</td>
</tr>
<tr>
<td>Update an existing order</td>
<td>PATCH</td>
<td>/orders/:orderId</td>
<td>Requires authentication</td>
<td>The request body needs to be in JSON format and allows you to update the following properties:<br><b>customerName</b> - String</td>
</tr>
<tr>
<td>Delete an existing order</td>
<td>DELETE</td>
<td>/orders/:orderId</td>
<td>Requires authentication</td>
<td>The request body needs to be empty</td>
<td></td>
</tr>
</table>

### API Authentication
***

To submit or view an order, API client need to be registered.<br>

Method: POST<br>
Endpoints: `/api-clients/`<br> 

The request body needs to be in JSON format and include the following properties:

 - `clientName` - String
 - `clientEmail` - String

 Example

 ```
 {
    "clientName": "Nolak",
    "clientEmail": "molak@example.com"
}
 ```

The response body will contain the access token. The access token is valid for 7 days.<br>
<br>**Possible error:**<br>
Status code 409 - "API client already registered." <br>

<b>Solution:</b> <br>Change the values for `clientEmail` and `clientName` to something else.

### Run Books API collection 
***

#### 1) Postman collection can be run in the postman runner
<ol>

#### Step-1:
Import the collection and csv file and run both files in postman runner<br>
</ol>

#### 2) Postman collection can be run in the command prompt
<ol> 

#### Step-1: Type in the command prompt:

Generate a report:<br>
`newman run Books_API_Test.postman_collection.json -d Book_Data.csv -r cli`
</ol>

#### 3) Postman collection can be run in newman
<ol>

#### 1. Newman HTML Report<br>
Open the cmd/terminal<br>
Install html reporter:<br>
`npm install -g newman-reporter-html`<br>
Generate html report:<br>
`newman run Books_API_Test.postman_collection -d Book_Data.csv -r html`
#### 2. Newman htmlextra report
Install the htmlextra package:<br>
```npm install -g newman-reporter-htmlextra```
<br>Generate htmlextra report:<br>
```newman run "Books_API_Test.postman_collection" -d Book_Data.csv -r htmlextra```
</ol>


