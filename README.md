# Router
Simple and complete PHP ROUTER
best for php 7.* or 8.*


How it works 

-> First create a .htaccess which send the requests to index.php 
   example: 
   RewriteEngine On
   RewriteCond %{REQUEST_FILENAME} !-f
   RewriteCond %{REQUEST_FILENAME} !-d
   RewriteRule . index.php [L]

-> Second create your index.php, and inport the class using include/require or by namespace, 
  if you have multiples namespace you can use the 
  composer autoload by simple creating a composer.json with this content:

  ..composer.json
  {
    "autoload": {
		"psr-4": 
        {
			    "Router\\": "Router/",
			     "etc\\": "etc/"	,
			      "folder1\\folder2\\": "folder1/folder1/"
        }
	   }
  }

  In your index.php

  $handler = new \Router\Requisition();
  $router = new \Router\Router();

  //start routes

  $router->get('/', function() use ($handler)
  {   
    $handler->handle($handler::CALLABLE,  "App\Controller\Home@indexAction" ,'Home/index');
  });

  //set up your 404 error page

  $router->set404(function()  use($handler){
    $handler->handle($handler::CALLABLE,  "App\Controller\E404@indexAction" ,"404/index");
  });


  //at end of index.php

 try
 {
     $router->run();
 }
 catch(Exception $e)
 {
     echo $e->getMessage();
 }
 
