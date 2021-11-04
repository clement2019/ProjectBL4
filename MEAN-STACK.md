    PROJECTS 4
    
BOOK RGISTER APPLICATION (MEAN -STACK IMPLEMENTATION)

Now that i have learned how to deploy LAMP, LEMP and MERN web stacks application in this project i got acquainted 

with MEAN stack application that i latter deployed to Ubuntu server. As can be seen below MEAN Stack is a mixture of following components modules:

•	MongoDB (Document database) – this keeps the data records and equally allows us to retrieve data.

•	Express (Back-end Software framework) – This sends requests to Database for Reads and Writes operations.

•	Angular (Front-end Software framework) – These deals with Client and Server Requests operations

•	Node.js (JavaScript runtime environment) – Accepts requests and displays results to end user

This task for this project is as shown below in this project i implemented a simple Book Register web interface

(graphic user interface) MEAN-stack. However, we can see that I made use of Node.js which is javaScrpit runtime built into chrome,

the Node.js was used to set up routes for the Expressjs and the Angular Controller.

In this project i created one Aws Ec2_instance of Ubuntu version 20.04 distribution with all the configurations for free tier set up.

I named the ec2 instance project4_fresh, while i connected to the instance using ssh connection using Gitbash.

I updated my ubuntu using the command below:

sudo apt update

![image](https://user-images.githubusercontent.com/55473846/140389482-dcaf6633-e8b8-47b0-ac0d-644c64a53d0a.png)

Once Ubuntu was updated, I now upgrade my ubuntu using the command below

Upgrade ubuntu

sudo apt upgrade


ADD CERTIFICATES

![image](https://user-images.githubusercontent.com/55473846/140389617-eb756f10-d897-4218-9ae4-b0ca4ce0a676.png)

I added Certificates by running the command below

sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates

curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

![image](https://user-images.githubusercontent.com/55473846/140389803-728cc7b7-2ff2-4037-baeb-36f53fe2cb01.png)


I now install NodeJS on my system using the command below

sudo apt install -y nodejs

![image](https://user-images.githubusercontent.com/55473846/140390197-273ceed4-8280-48d1-8947-94d250a445a6.png)

INSTALLING MONGODB

For this stage of the project i installed MongoDB for my data backed storage which will be in flexible JSON-LIKE documents, 

however this kind of documents can vary from one document type to the other while overtime we can change the database structure. In this project 

I added book data records to the Mongodb data storage system that has as columns book name, isbn number, author, and number of pages.

I now ran the command below

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6


echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list


![image](https://user-images.githubusercontent.com/55473846/140390516-255cc815-97fd-4cd2-9def-7cf6e28264fa.png)


I ran the command to install MongoDB as shown below 

sudo apt install -y mongodb

I started the server running command below

sudo service mongodb start

![image](https://user-images.githubusercontent.com/55473846/140390724-5f9bb225-909b-4151-8203-39c5b34782b1.png)

I verified that the service is up and running by running the command below

sudo systemctl status mongodb

![image](https://user-images.githubusercontent.com/55473846/140390957-f4535dfb-247b-4015-b413-99969dacb4a0.png)

I Installed npm – Node package manager by running the command below

sudo apt install -y npm

![image](https://user-images.githubusercontent.com/55473846/140391323-97f4cfd2-e10c-41b3-84fa-76a082e75ae5.png)

I Installed body-parser package as shown, but this needed because it will help me to process JSON files while pass in request to the server.

I ran the code as shown below

sudo npm install body-parser

![image](https://user-images.githubusercontent.com/55473846/140391660-e9154d46-05e4-4070-a0d3-4fcdfa49f860.png)

Now for the project proper I first created a folder named ‘Books’

mkdir Books && cd Books

In the Books directory, I Initialized npm project

npm init


![image](https://user-images.githubusercontent.com/55473846/140391803-75c72573-c005-4baa-b801-ac9f3d6ef56c.png)


![image](https://user-images.githubusercontent.com/55473846/140391908-4d0d78bd-9ffd-499e-8c6b-15e283ad0ca4.png)

I added a file to it named server.js

While I copied and paste the web server code below into the server.js file.

var express = require('express');
var bodyParser = require('body-parser');
var app = express();
app.use(express.static(__dirname + '/public'));
app.use(bodyParser.json());
require('./apps/routes')(app);
app.set('port', 3300);
app.listen(app.get('port'), function() {
    console.log('Server up: http://localhost:' + app.get('port'));
});



![image](https://user-images.githubusercontent.com/55473846/140392067-8e7a5b9c-645e-4e35-bab4-f84ea13781a0.png)


INSTALL EXPRESS AND SET UP ROUTES TO THE SERVER

 I Installed Express and set up routes to the server
 
Express is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.

I used Express in to passbook information to and from our MongoDB database.

I used Mongoose package which provides a straight-forward, schema-based solution to model your application data. I used Mongoose to establish a schema

for the database to store data of our book register.

![image](https://user-images.githubusercontent.com/55473846/140392213-f5f3d6eb-fdc0-488d-9cd9-97849b0da30e.png)

In ‘Books’ folder, create a folder named apps

mkdir apps && cd apps


I created a file named routes.js

vi routes.js


![image](https://user-images.githubusercontent.com/55473846/140392363-90e44e2f-8b88-45da-8b43-ae3cf962710a.png)

In the ‘apps’ folder, created a folder named models

mkdir models && cd models

Created a file named book.js

vi book.js

I copied and paste the code below into ‘book.js’

var mongoose = require('mongoose');
var dbHost = 'mongodb://localhost:27017/test';
mongoose.connect(dbHost);
mongoose.connection;
mongoose.set('debug', true);
var bookSchema = mongoose.Schema( {
  name: String,
  isbn: {type: String, index: true},
  author: String,
  pages: Number
});

var Book = mongoose.model('Book', bookSchema);

module.exports = mongoose.model('Book', bookSchema);

![image](https://user-images.githubusercontent.com/55473846/140395109-72ac039c-2a13-46d6-a790-0b8761c1b1a4.png)

Now i must access the routes with AngularJS

AngularJS provides a web framework for creating dynamic views in the web applications. In this project, i used AngularJS to connect

the web page with Express and perform actions on the book register.

I changed the directory back to ‘Books’

I created a folder named public

mkdir public && cd public

Add a file named script.js

vi script.js

I copied and paste the code below (controller configuration defined) into the script.js file.

var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $http) {
  $http( {
    method: 'GET',
    url: '/book'
  }).then(function successCallback(response) {
    $scope.books = response.data;
  }, function errorCallback(response) {
    console.log('Error: ' + response);
  });
  $scope.del_book = function(book) {
    $http( {
      method: 'DELETE',
      url: '/book/:isbn',
      params: {'isbn': book.isbn}
    }).then(function successCallback(response) {
      console.log(response);
    }, function errorCallback(response) {
      console.log('Error: ' + response);
    });
  };
  $scope.add_book = function() {
    var body = '{ "name": "' + $scope.Name + 
    '", "isbn": "' + $scope.Isbn +
    '", "author": "' + $scope.Author + 
    '", "pages": "' + $scope.Pages + '" }';
    $http({
      method: 'POST',
      url: '/book',
      data: body
    }).then(function successCallback(response) {
      console.log(response);
    }, function errorCallback(response) {
      console.log('Error: ' + response);
    });
  };
});

In public folder, create a file named index.html;

vi index.html

I copied and paste the code below into index.html file.

<!doctype html>
<html ng-app="myApp" ng-controller="myCtrl">
  <head>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
    <script src="script.js"></script>
  </head>
  <body>
    <div>
      <table>
        <tr>
          <td>Name:</td>
          <td><input type="text" ng-model="Name"></td>
        </tr>
        <tr>
          <td>Isbn:</td>
          <td><input type="text" ng-model="Isbn"></td>
        </tr>
        <tr>
          <td>Author:</td>
          <td><input type="text" ng-model="Author"></td>
        </tr>
        <tr>
          <td>Pages:</td>
          <td><input type="number" ng-model="Pages"></td>
        </tr>
      </table>
      <button ng-click="add_book()">Add</button>
    </div>
    <hr>
    <div>
      <table>
        <tr>
          <th>Name</th>
          <th>Isbn</th>
          <th>Author</th>
          <th>Pages</th>

        </tr>
        <tr ng-repeat="book in books">
          <td>{{book.name}}</td>
          <td>{{book.isbn}}</td>
          <td>{{book.author}}</td>
          <td>{{book.pages}}</td>

          <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
        </tr>
      </table>
    </div>
  </body>
</html>


![image](https://user-images.githubusercontent.com/55473846/140396183-62238c1c-a837-4b1f-92f4-4b1bed2a553a.png)

I changed the directory back up to Books

cd ..

Started the server by running this command:

node server.js

The server is now up and running, we can connect it via port 3300. You can launch a separate Putty or SSH console to test what curl command returns locally.

curl -s http://localhost:3300

As can be seen below I can view my book Register application of the public Ip address at port: 3300 as shown below,

I now can enter book details book name, isbn, Author, pages and it can be retrieved on the GUI interface

The application GUI was developed by the Angular front-end which help in capturing the data at the web interface. 

However, with the help of the Node.js which serve as the JavaScript runtime while the data was stored in MongoDB and the Expressjs serves as the backend framework

This ends the completion of the MEAN stack project

![image](https://user-images.githubusercontent.com/55473846/140396451-e50ee19a-add9-431b-a4cd-f292d0fb2def.png)

![image](https://user-images.githubusercontent.com/55473846/140396551-1d37ac3c-561b-4e55-9233-a1b94c77290f.png)


![image](https://user-images.githubusercontent.com/55473846/140396693-ac1ba88b-cc5c-4175-ba91-7e68403f75c9.png)


![image](https://user-images.githubusercontent.com/55473846/140396800-c4a6a9ea-26c0-4cd1-b641-a2f0fd3c4198.png)



