[![Build Status](https://travis-ci.org/thecommandline/ansible-role-nginx.svg?branch=master)](https://travis-ci.org/thecommandline/ansible-role-nginx)
# ansible-role-nginx

Set these variables if you wish to use the upstream [nginx.org](https://nginx.org/en/linux_packages.html) repositories. 
Leave them disabled to use distribution supplied nginx. The use_nginx_mainline variable will have no effect without use_nginx_repo.

    nginx_upstream_repo: no
    nginx_mainline: no

Variables used in top level nginx.conf and filesystem configuration. 

    nginx_sites_enabled: "/etc/nginx/sites-enabled" 
    nginx_sites_available: "/etc/nginx/sites-available" 
    nginx_user: www-data
    nginx_group: www-data 
    nginx_worker_processes: auto
    nginx_error_log: /var/log/nginx/error.log
    nginx_error_log_level: warn
    nginx_pid: /var/run/nginx.pid
    nginx_worker_connections: 1024
    nginx_default_type: application/octet-stream
    nginx_log_format_name: main
    nginx_log_format: | 
     '$remote_addr - $remote_user [$time_local] "$request" '
     '$status $body_bytes_sent "$http_referer" '
     '"$http_user_agent" "$http_x_forwarded_for"'
    nginx_access_log: /var/log/nginx/access.log
    nginx_access_log_format: main
    nginx_sendfile: "on"
    nginx_tcp_nopush: "off"
    nginx_keepalive_timeout: 65
    nginx_gzip: "off"

One or more server blocks can be defined by updating nginx_sites. Additionally an arbitrary number of locations may be added to each server. 

    nginx_sites:
      - server:
        file_name: ansible-default.conf
        listen: 80
        server_name: localhost
        root: "/var/www/ansible-default"
        locations1: {name: "/", uwsgi_pass: "django", include: "uwsgi_params"}
        locations2: {name: "/static/", alias: "/var/www/static"}
        locations3: {name: "/media/", alias: "/var/www/media"}

You may define an arbitrary number of upstream servers using the nginx_upstream_servers data structure. 

    nginx_upstream_servers:
      - server:
        file_name: "django-upstream.conf"
        upstream: {name: "django", type: "server", destination: "127.0.0.1:1111"}
## Warning

If you enable nginx_upstream_repo on a RedHat based operating system this role will remove the EPEL repository if installed due to it interfering with the use of the upstream nginx.org repository for nginx. 
