
🔧 Microservices Troubleshooting Guide
✅ MongoDB
Verify MongoDB service is running:

bash
Copy
Edit
netstat -lntp | grep mongod
Ensure the private IP address of MongoDB is correctly updated in the corresponding Route53 DNS record.

Check if remote access is allowed:

MongoDB should bind to 0.0.0.0 instead of 127.0.0.1 in the config file (/etc/mongod.conf):

yaml
Copy
Edit
bindIp: 0.0.0.0
✅ Catalogue
Verify the Catalogue service is running:

bash
Copy
Edit
netstat -lntp | grep catalogue
Ensure the private IP of the Catalogue service is updated in the corresponding Route53 record.

Review the catalogue.service file:

Confirm correct IP address, domain name, and port number are configured.

Check connectivity to dependent component:

Test connection to MongoDB:

bash
Copy
Edit
telnet <MONGODB-IP or DOMAIN> 27017
Verify that product data is loaded into MongoDB.

Ensure Catalogue’s IP or domain is correctly referenced in the frontend configuration file.

✅ Redis
Verify Redis service is running:

bash
Copy
Edit
netstat -lntp | grep redis
Confirm Redis private IP is updated in the Route53 DNS record.

Verify Redis allows remote access:

In /etc/redis/redis.conf:

conf
Copy
Edit
bind 0.0.0.0
Ensure protected mode is disabled:

conf
Copy
Edit
protected-mode no
✅ User
Verify User service is running:

bash
Copy
Edit
netstat -lntp | grep user
Ensure the private IP is updated in the Route53 DNS record.

Review the user.service file for correct:

IP address

Domain name

Port number

Check connectivity to dependencies:

Redis:

bash
Copy
Edit
telnet <REDIS-IP or DOMAIN> 6379
MongoDB:

bash
Copy
Edit
telnet <MONGODB-IP or DOMAIN> 27017
Confirm the User service IP/domain is updated in the frontend configuration.

✅ Cart
Verify Cart service is running:

bash
Copy
Edit
netstat -lntp | grep cart
Ensure Cart’s private IP is updated in the Route53 DNS record.

Check the cart.service file for:

Correct IP/domain

Port number

Verify connectivity to dependencies:

Redis:

bash
Copy
Edit
telnet <REDIS-IP or DOMAIN> 6379
Catalogue:

bash
Copy
Edit
telnet <CATALOGUE-IP or DOMAIN> 8080
Ensure Cart’s IP/domain is updated in the frontend configuration.

✅ MySQL
Verify MySQL service is running:

bash
Copy
Edit
netstat -lntp | grep mysql
Ensure MySQL private IP is correctly updated in Route53.

Check MySQL password handling:

Ensure secure storage and retrieval using environment variables or secrets manager.

✅ Shipping
Verify Shipping service is running:

bash
Copy
Edit
netstat -lntp | grep shipping
Ensure the private IP is updated in Route53.

Review the shipping.service file:

Confirm correct IP/domain and port number.

Check connectivity to dependencies:

MySQL:

bash
Copy
Edit
telnet <MYSQL-IP or DOMAIN> 3306
Cart:

bash
Copy
Edit
telnet <CART-IP or DOMAIN> 8080
Verify that shipping data is loaded into MySQL.

Ensure Shipping service IP/domain is updated in the frontend configuration.

✅ RabbitMQ
Verify RabbitMQ service is running:

bash
Copy
Edit
netstat -lntp | grep rabbitmq
Ensure RabbitMQ’s private IP is updated in Route53.

Validate RabbitMQ credentials and permissions:

Check username, password, and access control:

bash
Copy
Edit
rabbitmqctl list_users
rabbitmqctl list_permissions
✅ Payments
Verify Payments service is running:

bash
Copy
Edit
netstat -lntp | grep payment
Confirm that the private IP is updated in Route53.

Review the payment.service file:

Check for correct IP/domain and port number.

Check connectivity to dependencies:

User:

bash
Copy
Edit
telnet <USER-IP or DOMAIN> 8080
RabbitMQ:

bash
Copy
Edit
telnet <RABBITMQ-IP or DOMAIN> 5672
Cart:

bash
Copy
Edit
telnet <CART-IP or DOMAIN> 8080
Ensure the Payments service IP/domain is updated in the frontend configuration.


✅ Frontend
Verify Frontend service is running:

bash
Copy
Edit
netstat -lntp | grep nginx
Ensure the public IP address of the Frontend is correctly updated in its respective Route53 DNS record.

Review the nginx.conf file:

Confirm all component IP addresses, domain names, and port numbers are correctly configured.

Check connectivity from Frontend to its dependent services:

bash
Copy
Edit
telnet <CATALOGUE-IP or DOMAIN> 8080
telnet <USER-IP or DOMAIN> 8080
telnet <CART-IP or DOMAIN> 8080
telnet <SHIPPING-IP or DOMAIN> 8080
telnet <PAYMENT-IP or DOMAIN> 8080