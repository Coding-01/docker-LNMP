FROM zhangpengzhan456/centos:7.4.1708
LABEL MAINTAINER="2775147135@qq.com"
RUN set -x; \
    rm -rf /etc/yum.repos.d/{CentOS-CR.repo,CentOS-Debuginfo.repo,CentOS-fasttrack.repo,CentOS-Media.repo,CentOS-Sources.repo,CentOS-Vault.repo}

ENV TZ "Asia/Shanghai"

RUN echo "nameserver 8.8.8.8" >>/etc/resolv.conf \
    && yum -y install gcc automake autoconf libtool make gcc-c++ vixie-cron \
wget zlib  file openssl-devel sharutils zip  bash vim cyrus-sasl-devel \
libmemcached libmemcached-devel libyaml libyaml-devel unzip libvpx-devel \
openssl-devel ImageMagick-devel  autoconf  tar libxml2-devel gd-devel \
libmcrypt-devel libmcrypt mcrypt mhash libmcrypt libmcrypt-devel libxml2 \
libxml2-devel bzip2 bzip2-devel curl curl-devel libjpeg libjpeg-devel libpng \
libpng-devel freetype-devel bison libtool-ltdl-devel net-tools \
    && yum clean packages && yum clean headers && yum clean all

RUN [ ! -d /opop ] && mkdir /opop && cd /opop \
    && wget http://nginx.org/download/nginx-1.9.7.tar.gz \
    && tar xzf nginx-1.9.7.tar.gz \
    && cd /opop/nginx-1.9.7 \
    && ./configure --prefix=/usr/local/nginx --with-http_ssl_module --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_gzip_static_module --with-http_stub_status_module --with-debug \
    &&  make && make install

#配置nginx
ENV HTTP_PHP_CONFIG \\\n\\\t#php\\\n\\\tlocation ~ \\\\.php$ {\\\n\\\t\\\troot    html;\\\n\\\t\\\tfastcgi_pass   php7:9000;\\\n\\\t\\\tfastcgi_index    index.php;\\\n\\\t\\\tfastcgi_param  SCRIPT_FILENAME    /usr/local/nginx/html\$fastcgi_script_name;\\\n\\\t\\\tinclude    fastcgi_params;\\\n\\\t}\\\n\\\n\\\t

RUN sed -i -e "s@# deny access to .htaccess files, if Apache@${HTTP_PHP_CONFIG}# deny access to .htaccess files, if Apache@" /usr/local/nginx/conf/nginx.conf 

EXPOSE 80 443

#启动nginx
ENTRYPOINT ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]



#BUILD
    docker build -t nginx:1.9.7 .


Usage:
#创建你本机的php代码路径(要和PHP的容器挂载为同一个目录 ! ! !)
    mkdir /data
#Create Container
    docker run --name nginx -p 80:80 -v /data:/usr/local/nginx/html --link php7:php7 -itd nginx:1.9.7
