# Enabling-SSL-for-HTTP-and-bolt-for-Neo4j-4.x



Edit neo4j.conf
```
## Enable Bolt connector over TLS
dbms.connector.bolt.enabled=true
dbms.connector.bolt.tls_level=REQUIRED

#Disable HTTP Connector. There can be zero or one HTTP connectors.**
dbms.connector.http.enabled=false

# Enable HTTPS Connector. There can be zero or one HTTPS connectors
dbms.connector.https.enabled=true
dbms.connector.https.listen_address=:7473
dbms.connector.https.advertised_address=:7473

## Bolt SSL configuration
dbms.ssl.policy.bolt.enabled=true
dbms.ssl.policy.bolt.base_directory=certificates/bolt
dbms.ssl.policy.bolt.private_key=private.key
dbms.ssl.policy.bolt.public_certificate=public.crt
dbms.ssl.policy.bolt.client_auth=NONE

## Https SSL configuration
dbms.ssl.policy.https.enabled=true
dbms.ssl.policy.https.base_directory=certificates/https
dbms.ssl.policy.https.private_key=private.key
dbms.ssl.policy.https.public_certificate=public.crt
dbms.ssl.policy.https.client_auth=NONE
```

## set your ip
![image](https://user-images.githubusercontent.com/77326619/161441019-4efc69ec-cf9a-4302-a5e9-8f49953d7249.png)

![image](https://user-images.githubusercontent.com/77326619/161441040-7813c003-a778-44ab-b30d-5aded40330e3.png)

## Create directory in <NEO4J HOME>
mkdir certificates
mkdir certificates/https
mkdir certificates/https/trusted
mkdir certificates/https/revoked
mkdir certificates/bolt
mkdir certificates/bolt/trusted
certificates/bolt/revoked
 
![image](https://user-images.githubusercontent.com/77326619/161441080-794893c4-828a-4696-beb0-62f909f6456e.png)

## Create new key
```
openssl req -x509 -newkey rsa:2048 -keyout private.key -out public.crt -nodes -days 1000
```
 
![image](https://user-images.githubusercontent.com/77326619/161441163-eedf12b6-381f-4375-a893-9185f19bed0b.png)

 
 ## Copy a private key to directory certificates
```
cp private.key certificates/bolt
cp public.crt certificates/bolt
cp private.key certificates/https
cp public.crt certificates/https
service neo4j restart 
```
![image](https://user-images.githubusercontent.com/77326619/161441226-91f19b13-85dd-4088-881e-410e83658958.png)

## Login into cypher use command
  
```
cypher-shell -a neo4j+ssc://0.0.0.0:7687
```
![image](https://user-images.githubusercontent.com/77326619/161441289-3b68fd8a-1d96-4c20-a808-f555f5386575.png)
  
  
  
## Open browser and open https://0.0.0.0:7687
  ![image](https://user-images.githubusercontent.com/77326619/161441330-e79818b6-e38b-4f96-9e99-297d177aebbe.png)

