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

http://download.osgeo.org/
http://download.osgeo.org/

https://ftp.postgresql.org/pub/source/v12.1/postgresql-12.1.tar.gz
https://ftp.postgresql.org/pub/source/v12.1/postgresql-12.1.tar.bz2
https://download.osgeo.org/proj/proj-5.1.0.tar.gz
http://download.osgeo.org/geos/geos-3.6.4.tar.bz2
http://download.osgeo.org/gdal/2.4.3/gdal-2.4.3.tar.gz
http://download.osgeo.org/postgis/source/postgis-3.0.0.tar.gz
http://download.osgeo.org/postgis/source/postgis-3.0.0rc2.tar.gz


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
 
 
 
 
 
 
 ----------------------------------------------------------------------------------------------------------------------------------------------------------------
 创建组和用户

groupadd postgres
useradd -g postgres -G postgres -d /home/postgresql postgres

解压、安装、编译
bunzip2 postgresql-12.1.tar.bz2
tar -xvf ./postgresql-12.1.tar
----------------------------------------    tar -xf /opt/postgresql-12.1.tar.gz
cd postgresql-12.1
./configure --prefix=/usr/share/postgresql-12
make && make install

配置环境变量
vi /etc/profile
export PGHOME=/usr/share/postgresql-12/
export PGDATA=/data/pgsql-12
export PATH=$PGHOME/bin:$PATH
export LANG=en_US.utf8
export LD_LIBRARY_PATH=$PGHOME/lib:$LD_LIBRARY_PATH
source /etc/profile
PS：
针对当前特定的用户起作用的环境变量修改bashrc文件，这种方法更为安全，它可以把使用这些环境变量的权限控制到用户级别，这里是针对某一特定的用户，如果你需要给某个用户权限使用这些环境变量，你只需要修改其个人用户主目录下的 .bashrc文件就可以了。

vi ~/.bashrc



配置文件权限

mkdir -p /data/pgsql-12

chown -R postgres:postgres /data/pgsql-12

chown -R postgres:postgres /usr/share/postgresql-12

passwd postgres
admin

初始化

su - postgres

initdb -E utf8 -D $PGDATA

启动

cd /data/pgsql-12

pg_ctl -D /data/pgsql-12/ -l logfile start

修改配置启动脚本

cd /usr/share/postgresql-12/bin

启动pg_ctl -D /data/pgsql-12/ -l logfile start
su    切换root
cp /opt/postgresql-12.1/contrib/start-scripts/linux /etc/init.d/postgresql-12
chmod 777 /etc/init.d/postgresql-12
sed -i '/prefix=/s#prefix=.*#prefix=/usr/share/postgresql-12#' /etc/init.d/postgresql-12
sed -i 's#PGDATA=.*#PGDATA=/data/pgsql-12#' /etc/init.d/postgresql-12
启停
/etc/init.d/postgresql-12 start  
/etc/init.d/postgresql-12 stop
配置远程
echo -e "listen_addresses = '*'\nmax_connections = 100">>/data/pgsql-12/postgresql.conf

设置开机自启动

chmod 777 /etc/rc.d/rc/local
echo '/etc/init.d/postgresql-12 stop
/etc/init.d/postgresql-12 start'>>/etc/rc.d/rc/local
启动检查

/etc/init.d/postgresql-12 start
ps -ef|grep post
登陆
su - postgres
psql
修改密码
alter user postgres with password 'admin';

create user test_user with password 'admin';            // 创建用户
create database test_db owner test_user;                 // 创建数据库
grant all privileges on database test_db to test_user;   // 授权
exit

------------------------------------------------------------------------------------------------------------------------

su    切换 root
tar -xf gdal-3.0.2.tar.gz
tar -xf postgis-3.0.0rc2.tar.gz
tar -jxf geos-3.6.1.tar.bz2
tar -jxf geos-3.8.0rc3.tar.bz2
tar -xf proj-6.2.1.tar.gz

mkdir /usr/share/postgresql-12/plugin


---------------------------------------------------------------------------------------------------------
