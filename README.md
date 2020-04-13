# nginx restream server
Instructions for setting up an NGINX server to ingest rtmp streams and restream them to multiple platforms (Youtube, Twitch, Facebook, Instagram, etc.)

## NOTE: this readme is a work in progress.

INSTALL
------------------------------------------------
// update packages
apt-get update

// upgrade
apt-get upgrade

// Get NGINX tar ball
wget http://nginx.org/download/nginx-1.16.1.tar.gz

// Unzip it
tar xzf nginx-1.16.1.tar.gz

// to use git
apt-get install git

// Clone the RTMP module from git
git clone git://github.com/arut/nginx-rtmp-module.git

// CD into nginx directory
cd nginx-1.16.1

// to compile
apt-get install gcc

// PCRE library
apt-get install libpcre3 libpcre3-dev build-essential libssl-dev

// zlib
apt-get install --reinstall zlibc zlib1g zlib1g-dev

// compile it
./configure --add-module=/root/nginx-rtmp-module

// make
make

// install package just made
make install

// what version?
/usr/local/nginx/sbin/nginx -v

// start nginx
/usr/local/nginx/sbin/nginx

// stop nginx
/usr/local/nginx/sbin/nginx -s stop

// Edit conf
nano /usr/local/nginx/conf/nginx.conf

** See nginx.conf file **

// start nginx after editing conf
/usr/local/nginx/sbin/nginx



STUNNEL
------------------------------------------------
# start
stunnel /etc/stunnel/stunnel.conf
/usr/bin/stunnel /etc/stunnel/stunnel.conf

# kill
/usr/bin/pkill stunnel

# stunnel.key
/etc/stunnel/stunnel.key

# stunnel.crt
/etc/stunnel/stunnel.crt

# stunnel.pem
/etc/stunnel/stunnel.pem

# /etc/stunnel/stunnel.conf
########################################
# Enable proper SSL security.  Without this, you are completely insecure!
verify = 2
CAfile = /etc/ssl/certs/ca-certificates.crt
cert = /etc/stunnel/stunnel.pem

setuid = stunnel4
setgid = stunnel4
pid=/tmp/stunnel.pid
output = /var/log/stunnel4/stunnel.log
include = /etc/stunnel/conf.d



# /etc/stunnel/conf.d/fb.conf
########################################

# Enable proper SSL security.  Without this, you are completely insecure!
verify = 2
CAfile = /etc/ssl/certs/ca-certificates.crt

[fb-live]
client = yes
accept = [your-ip-address]:19350
connect = live-api-s.facebook.com:443
verifyChain = no


INSTAGRAM
------------------------------------------------
Directly into Instagram
rtmps://live-upload.instagram.com:443/rtmp/[stream-key]

First to our server, then to instagram via stunnel
rtmp://[your-ip-address]:19350/rtmp/[your-ig-stream-key]
#NOTE: this isn't tested yet - may need more config


FACEBOOK
------------------------------------------------
Directly into facebook
rtmps://live-api-s.facebook.com:443/rtmp/[your-facebook-stream-key]

First to our server, then to facebook via stunnel
rtmp://[your-ip-address]:19350/rtmp/[your-fb-stream-key]



TWITCH ACCOUNT
------------------------------------------------
rtmp://live.twitch.tv/app/[your-twitch-stream-key]



YOUTUBE ACCOUNT
------------------------------------------------

rtmp://a.rtmp.youtube.com/live2/[your-youtube-stream-key]

