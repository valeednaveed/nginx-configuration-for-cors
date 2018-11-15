# nginx-configuration-for-cors
Solution of no access control allowed origin error using forward proxy and nginx 

#Commands to install and run nginx (ubuntu) 

sudo apt-get install nginx 
sudo apt-get update 


#check status of nginx
systemctl status nginx      

#restart nginx
systemctl restart nginx   

#open default configuration file 
sudo emacs /etc/nginx/sites-available/default


#Congiguration 
#--------------------------------------------------------------------------------------------------------------

server {
	listen 80 default_server;
	listen [::]:80 default_server;



	root /var/www/html;

	# Add index.php to the list if you are using PHP
	index index.html index.htm index.nginx-debian.html;

	server_name _;

	location / {
		# First attempt to serve request as file, then
		# as directory, then fall back to displaying a 404.
		try_files $uri $uri/ =404;
	}

	location /web {
	     if ($request_method = 'GET') {
                add_header 'Access-Control-Allow-Origin' '*';
                add_header 'Access-Control-Allow-Methods' 'GET,PUT, POST,DELETE';
             }

 	     if ($request_method = 'PUT') {
                add_header 'Access-Control-Allow-Origin' '*';
                add_header 'Access-Control-Allow-Methods' 'GET,PUT, POST,DELETE';
             }

	     if ($request_method = 'POST') {
                add_header 'Access-Control-Allow-Origin' '*';
                add_header 'Access-Control-Allow-Methods' 'GET,PUT, POST,DELETE';
             }

	    if ($request_method = 'DELETE') {
                add_header 'Access-Control-Allow-Origin' '*';
                add_header 'Access-Control-Allow-Methods' 'GET,PUT, POST,DELETE';
             }
           
	    

	     proxy_pass http://facebook.com;
  
	}

}









