# Geo balancing with NGINX
It's pet project for practicing with geo balancin using NGINX. The goal is to set nginx server which balance requests based on user IP through 3 geo zones (US,UK,Other).

### Tools
* nginx-more [https://github.com/shashwot/nginx-more]
* GeoLite2 database from the Maxmind [https://dev.maxmind.com/geoip/geolite2-free-geolocation-data]
* docker compose

### Run
To run the infrastrucutre - start the docker compose with command in the root of project:
``` docker compose up ```

### NGINX Urls
* / - home page to test is NGINX runs;
* /info/country - shows what country NGINX determine based on user IP;
* /info/addr    - your IP address that NGINX define;
* /geoip        - balancing endpont, the result based on your geo zone;

### Workaround
The project may not work locally as NGINX will define all local requests with local IP address. 
To workaround this - you may set variables inside the NGINX to hardcode IP to process with command
```
map "" $test_ip {
     default 8.8.8.8;
}

geoip2 /var/lib/GeoIP/GeoLite2-Country.mmdb {
    $geoip2_data_country_iso_code source=$test_ip country iso_code;
}
```