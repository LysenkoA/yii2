# yii2

install

<hr>

<h1>ROUTING</h1>

<h2>Add .htaccess</h2>

<pre>
  Options +FollowSymLinks
  IndexIgnore */*
  RewriteEngine on
   
  # if request begins with /admin remove admin and ad /backend/web/
  RewriteCond %{REQUEST_URI} ^/admin
  RewriteRule ^admin/?(.*) /backend/web/$1
   
  # other requests add /frontend/web/$1
  RewriteCond %{REQUEST_URI} !^/(frontend/web|backend/web|admin)
  RewriteRule (.*) /frontend/web/$1
   
  # if frontend request 
  RewriteCond %{REQUEST_URI} ^/frontend/web
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /frontend/web/index.php 
   
  # if backend request
  RewriteCond %{REQUEST_URI} ^/backend/web
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /backend/web/index.php 
</pre>

<h2>Add to backend/config/main.php</h2>

<pre>
  'urlManager' => [
      'enablePrettyUrl' => true,
      'showScriptName' => false,
      'enableStrictParsing' => true,
      'rules' => [
          [
              'pattern' => '',
              'route' => 'site/index',
              'suffix' => ''
          ],
          [
              'pattern' => '<controller>/<action>',
              'route' => '<controller>/<action>',
              'suffix' => ''
          ],
      ],

  ],
  'request' => [
      'baseUrl' => '/admin'
  ],
</pre>

<h2>Add to frontend/config/main.php</h2>

<pre>
'urlManager' => [
    'enablePrettyUrl' => true,
    'showScriptName' => false,
    'enableStrictParsing' => true,
    'rules' => [
         [
             'pattern' => '',
             'route' => 'site/index',
             'suffix' => '',
         ],
         [
             'pattern' => '<controller>/<action>',
             'route' => '<controller>/<action>',
             'suffix' => ''
         ],
    ],
],
'request' => [
    'baseUrl' => '',
],   
</pre>
