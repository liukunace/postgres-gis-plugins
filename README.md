# postgres-gis-plugins
postgres-gis-plugins &lt; c++11

yum install -y readline-devel zlib-devel make gcc

sudo yum install -y readline readline-devel openssl openssl-devel zlib zlib-devel
make版本3.80或以上
make --version
yum -y install libxml2-devel

yum install -y gcc build-essential
yum install -y gcc gcc-c++ autoconf automake
yum -y install zlib zlib-devel openssl openssl-devel pcre pcre-devel 
yum -y install gcc gcc-c++ autoconf libjpeg libjpeg-devel libpng libpng-develfreetype freetype-devel libxml2 libxml2-devel zlib zlib-devel glibc glibc-develglib2 glib2-devel bzip2 bzip2-devel ncurses ncurses-devel curl curl-devele2fsprogs e2fsprogs-devel krb5 krb5-devel libidn libidn-devel opensslopenssl-devel openldap openldap-devel nss_ldap openldap-clientsopenldap-servers
make && make install   ok 



tar -xf   5.1.0止需要c++11环境
cd /opt/proj-6.2.1
./configure --prefix=/usr/share/postgresql-12/plugin/proj
make && make install
echo "/usr/share/postgresql-12/plugin/proj/lib" > /etc/ld.so.conf.d/proj-5.1.0.conf
ldconfig

ln -s /usr/local/gmp-6.1.0 /usr/local/gmp

http://download.osgeo.org/proj/proj-6.3.0RC1.tar.gz
 
ar -xf   3.6.4止需要c++11环境

cd /opt/geos-3.8.0rc3
 ./configure --prefix=/usr/share/postgresql-12/plugin/geos
make && make install
 echo "/usr/share/postgresql-12/plugin/geos/lib" > /etc/ld.so.conf.d/geos-3.6.4.conf
 ldconfig

gdal-2.4.3止需要c++11环境

 cd /opt/gdal-3.0.2   --configure: error: PROJ 6 symbols not found
./configure --with-proj=/usr/share/postgresql-12/plugin/proj --prefix=/usr/share/postgresql-12/plugin/gdal/
make && make install
 echo "/usr/share/postgresql-12/plugin/gdal/lib" > /etc/ld.so.conf.d/gdal-2.4.3.conf
 ldconfig


./configure --prefix=/usr/share/postgresql-12/plugin/postgis --with-pgconfig=/usr/share/postgresql-12/bin/pg_config --with-geosconfig=/usr/share/postgresql-12/plugin/geos/bin/geos-config --with-gdalconfig=/usr/share/postgresql-12/plugin/gdal/bin/gdal-config --with-projdir=/usr/share/postgresql-12/plugin/proj

No package 'json-c' found
yum install json-c json-c-devel

 cd /opt/postgis-3.0.0rc2
 ./configure --prefix=/usr/share/postgresql-12/plugin/postgis --with-pgconfig=/usr/share/postgresql-12/bin/pg_config --with-geosconfig=/usr/share/postgresql-12/plugin/geos/bin/geos-config --with-gdalconfig=/usr/share/postgresql-12/plugin/gdal/bin/gdal-config --with-projdir=/usr/share/postgresql-12/plugin/proj
make && make install
 echo "/usr/share/postgresql-12/plugin/postgis/lib" > /etc/ld.so.conf.d/postgis-3.0.0.conf
 ldconfig
 
 
 
