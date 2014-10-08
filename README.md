eAccess Mobile - Developer Guide
=========

Please install & run ``` Markdown Preview ``` in your sublime package manager to view this guide in HTML form

Version
-------

0.1 - Inital Version 10/02/2014, Xi Lin

Tech
-----------

The following are the big tech stacks we frequently used for building this application:

* [AngularJS] - MVC framework for data-binding, front-end routing, and awesomeness
* [UI-router] - Client side URL routing
* [UI-Bootstrap] - UI boilerplate framework built on top of angularjs
* [Less] - CSS preprocessor
* [Jasmine] - Javascript unit testing
* [Yeoman] - Scaffolding tool that includes grunt.js and bower.js - requires nodejs installed
* [Grunt.js] - Code automation tool
* [Bower.js] - front-end component repository
* [Node.js] - build environment
* [SublimeText3] - awesome text-editor


QuickStart
------------

####Installation
* Download and install Nodejs
* Set Up Proxy in environmental variables:
>HTTP_PROXY   http://proxy.usps.gov:8080
>HTTPS_PROXY  https://proxy.usps.gov:8080
```
####Install yeoman
npm install -g yo
```
* Download the SVN Repository into local folders - a development copy, and a staging copy for deployment.

####Deployment
```
#Run unit test
grunt test
#Run build process
grunt build
```
* Zip CONTENT of dist folder and upload to unix personal server
* Run deployment script

####Routing

Routing ties urls/app-states to html partials with controllers, and display content accordingly.

* Setup for the router is declared in the app startup file - app.js (```*.otherwise('/login')```)

* Routing is configured by the UI router, and exists in the module configuration files (ie. ```*-module.js```).

* Dependency injection in app.js allows the entire application access to module-level routing. 

####Creating new files

```sh
# Yeoman - cg-angular (scaffolding generator)
yo cg-angular:directive my-awesome-directive
yo cg-angular:partial my-partial
yo cg-angular:service my-service
yo cg-angular:filter my-filter
yo cg-angular:module my-module
yo cg-angular:modal my-modal
```
###Task Automation
```sh
# Grunt
grunt serve   #This will run a development server.
grunt test    #Run local unit tests.
grunt build   #Places a fully optimized (minified, concatenated, and more) in /dist
```

App Configuration Files
-----------------
* ```/Gruntfile.js``` [create automation taskings]
* ```/package.json```[npm (node repository manager) tools and dependencies]
* ```/bower.json``` [framework versioning and dependencies]
* ```/.editorconfig``` [Editor configuration]
* ```/.bowerrc``` [Bower config]
* ```/.jshintrc``` [JS Hint configuration]
* ```/.yo-rc.json``` [Yeoman generator configuration]
* ```/shared-module/APPCONSTANT.js``` [application settings and configuration]

Code Structure Overview
-----------
####The structure of the codebase is as follows:

```sh
 Mobile Web ......................... Root folder
    /bower_components  .............. Client side libraries managed by bower
    /dist ........................... Distributable version of app built using grunt and Gruntfile.js
    /images  ........................ Client side images
    /node_modules  .................. Npm managed libraries used by grunt
    /src ............................ Source folder for all eAccess modules
        /approval-screen-module  .... Manages FSC, and MGR screens
        /header-footer-module  ...... Manages Header bar
        /home-module  ............... Placeholder for the pending actions routing
        /login-module  .............. Manages the login screen
        /notification-module  ....... Manages the notification globe on the header bar
        /password-module  ........... Manages all password screen - on login, and in user profile
        /pending-approval-module  ... Manages the listing of all pending actions - MGRs & FSCs
        /router-module  ............. Contain the application templating and base routes, along with the slide-menu
        /shared-module  ............. Commonly used services and functionalities - ie SessionManager, ApiService, AppContstants
        /user-access-module  ........ Contains screens related to user requests
        /user-module  ............... Contains screens related to user listings
    /index.html  .................... Provides source for the build process, and can determines which files wil be in the build
    /app.js ......................... Application entry point, creates application module and provides default routing
    /app.less  ...................... Main app-wide styles
```    
####Example module structure
```sh
/my-module .......................... top-level module folder
	/partial ........................ top-level folder for all partials
		/my-partial ................. partial folder
			/my-partial-spec.js ..... unit test for controller
			/my-partial.html ........ html of partial
			/my-partial.js .......... controller file for partial
			/my-partial.less ........ css styles for partial
	/directive ...................... top-level directive folder
		/my-directive-spec.js ....... unit test for directive
		/my-directive.js ............ directive file
	/my-modal ....................... specific modal folder
		/my-modal.spec .............. unit testing for modal controller
		/my-modal.html .............. modal html
		/my-modal.js ................ modal controller
		/my-modal.less .............. modal styles
	/service ........................ top-level service folder
		/my-service-spec.js ......... unit test for the service
		/my-service.js .............. service
	/my-module.js ................... module routing configuration
	/my-modal.less .................. module-wide styles
```

Code Conventions
----------------

####File Creation
* Use command line to create files/folders (yo cg-angular:<fileType> <fileName>)
* all lower-case
* hyphens for multiple words
* include file type in name: ie. approval screen = approval-module, approval-partial, approval-service
* Develop and Build in separate SVN folders - have a staging and development copy of the repository


####Internal names
* Module names should be camelBack with  first letter uppercased - and must contain type: ie. ApprovalModule
* Controllers must be camelBack with first letter lowercased - and must contain type: ie approvalCtrl

####Functional Conventions
* Controller should not be bind to the partial html - but in the router.
* DOM manipulation should be kept to directive - as much as functionally possible
* Data-driven UI changes should be bind to $scope.ui for clarity (Such as ng-If/ng-Show - ng-If="ui.changed")
* Services should used to move data between controllers (Use ```/SharedApiServices.js```)

Useful Resources
----------------
####Sublime Plugins - Require Package Control
[Package Control] - Sublime Plugin repository.

* Side Bar - provides a more functional side bar directory view
* Javascript Beautify - formats javascript
* Bracket Hightlighter - highlighting of html and javascript

####How to grok Angular

* [Egghead.io] - Short videos on angular basics

[SublimeText3]:http://www.sublimetext.com/
[UI-router]:https://github.com/angular-ui/ui-router
[Less]:http://lesscss.org/
[Jasmine]:http://jasmine.github.io/
[UI-Bootstrap]:http://angular-ui.github.io/bootstrap/
[AngularJS]:https://angularjs.org/
[Yeoman]:http://yeoman.io/
[Grunt.js]:http://gruntjs.com/
[Bower.js]:http://bower.io/
[Node.js]:http://nodejs.org/
[Package Control]:https://sublime.wbond.net/
[Egghead.io]:http://egghead.io
