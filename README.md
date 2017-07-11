# docker-nginx
Nginx docker image for CloudEstuary.com

This image based on official nginx image and configured to play nice with php-fpm.

It replaces the default nginx configuration to send all php requests in fpm container defined in environment.

# Additional supported variables

`CLIENT_MAX_BODY_SIZE`: max request size.
`DOCUMENT_ROOT`: document root
`INDEX_FILE`: index file name within document root
`PHP_FPM`: fpm containar name or alias (acessible via container`s network)

# docker-compose example

~~~
nginx:
        image: 'cloudestuary/nginx:mainline-fpm'
        environment:
            CLIENT_MAX_BODY_SIZE: 100m
            DOCUMENT_ROOT: /var/www/html/public
            INDEX_FILE: index.php
            PHP_FPM: app
        networks:
            - app
        volumes:
            - './:/var/www/html'
app:
        image: 'cloudestuary/php-fpm:7.1'
        environment:
            MAX_UPLOAD_FILE_SIZE: 100m
        networks:
            - app
        volumes:
            - './:/var/www/html'
~~~
