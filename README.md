Mini presentation about caching proxy server squid3

1. Create instance (Ubuntu) (example: Vscale)
2. Connect via ssh
3. sudo apt-get update
4. sudo apt-get install squid apache2-utils
5. cd /etc/squid3/
6. sudo cp squid.conf squid.conf.backup
7. sudo nano squid.conf
8. Add to top

Example configuration

```
# Set network adress and port for Squid
http_port 3128 

# Create Access Control List for all adresses
acl all src 0.0.0.0/0.0.0.0

# Block mp3 files for download
acl mp3_ext url_regex -i \.mp3$
http_access deny mp3_ext

# Block bad url
acl bad_url dstdomain vk.com
acl bad_url dstdomain twitter.com
http_access deny bad_url

# Add basic params for atuh
auth_param basic program /usr/lib/squid3/basic_ncsa_auth /etc/squid3/passwd
# Count process for uthenticate programm
auth_param basic children 2
# String for window uthorization name
auth_param basic realm My Proxy Server
# Set expiretime for saving pair of login/password
auth_param basic credentialsttl 2 hours
# Case sensetive
auth_param basic casesensitive off

# Set anonimazed proxy
via off
forwarded_for off

# Default open window for login/password
acl users proxy_auth REQUIRED

# Auth parametres for group
http_access deny !users
http_access allow users

# Download max size
reply_body_max_size 10 Mb

```
9. sudo touch /etc/squid3/passwd
10. sudo htpasswd /etc/squid3/passwd admin
11. service squid3 restart
12. dpkg -L squid3 | grep ncsa_auth
13. Links
    - http://wilson18.com/topic/48-how-to-create-your-own-squid-private-proxy-on-a-vpsdedicated-server/
    - http://habrahabr.ru/post/217629/
    - http://www.zyxmon.org/2014/02/21/ustanavlivaem-anonimnyj-proxy-na-vps/
    - https://evgit.com/linux/podnimaem-vysoko-anonimnyy-http-proksi-s-bazovoy-avtorizaciey-ispolzuya-squid-na-vps-s-debian
    - https://evgit.com/linux/podnimaem-vysoko-anonimnyy-http-proksi-s-bazovoy-avtorizaciey-ispolzuya-squid-na-vps-s-debian
