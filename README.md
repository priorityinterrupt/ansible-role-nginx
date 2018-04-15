# ansible-role-nginx

Set these variables if you wish to use the upstream nginx.org repositories. 
Leave them disabled to use distribution supplied nginx. The use_nginx_mainline variable will have no effect without use_nginx_repo.

    nginx_nginxorg_repo: no
    nginx_nginxorg_mainline: no

Variables used in top level nginx.conf and filesystem configuration.

    nginx_conf_root: /etc/nginx
    nginx_sites_enabled: "{{ nginx_conf_root }}/sites-enabled" 
    nginx_sites_available: "{{ nginx_conf_root }}/sites-available" 
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

## Warning

If you enable nginx_nginxorg_repo on a RedHat based operating system this role will remove the EPEL repository if installed due to it interfering with the use of the nginx.org repository for nginx. 