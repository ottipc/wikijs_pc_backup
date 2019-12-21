<!-- TITLE: Fsbadmin -->
<!-- SUBTITLE: A quick summary of Fsbadmin -->

# Header


npm install -g create-react-app

npm install -g npm

create-react-app fsb-admin

Install yarn : https://yarnpkg.com/lang/en/docs/install/#debian-stable
yarn add react-admin ra-data-json-server prop-types



yarn start



CORS APACHE in 443 :
  #CORS REwrite
        RewriteEngine On
        RewriteCond %{REQUEST_METHOD} OPTIONS
        RewriteRule ^(.*)$ $1 [R=200,L]

 
 #CORS
        Header always set Access-Control-Allow-Origin "*"
        Header always set Access-Control-Allow-Methods "POST, GET, OPTIONS"

