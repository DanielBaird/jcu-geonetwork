# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  # config.vm.box = "chef/centos-6.6"
  config.vm.box = "puppetlabs/centos-6.6-64-nocm"

  config.vm.network "public_network", bridge: "en2: Thunderbolt Ethernet"
  config.vm.network "forwarded_port", guest: 80, host: 9090

  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.provider "virtualbox" do |vb|
    # vb.gui = true
    vb.memory = "3000"
  end

  config.vm.provision "shell", inline: <<-SHELL
    yum -y check-update # apt-get -y -q update
    # apt-get -y -q install software-properties-common htop

    # -- make the geonetwork and eresearch users -----
    useradd geonetwork
    useradd eresearch

    # -- get java (openJDK 7 is okay for geonetwork) -----
    # apt-get -y -q install openjdk-7-jre
    yum install -y java-1.7.0-openjdk
    # add JAVA_HOME env var for the two users
    echo " " >> /home/eresearch/.profile
    echo " " >> /home/geonetwork/.profile

    echo "export JAVA_HOME=/usr/lib/jvm/java-7-oracle" >> /home/eresearch/.profile
    echo "export JAVA_HOME=/usr/lib/jvm/java-7-oracle" >> /home/geonetwork/.profile

    # # -- get geoserver -----
    # wget -q http://downloads.sourceforge.net/project/geoserver/GeoServer/2.7.1.1/geoserver-2.7.1.1-bin.zip?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fgeoserver%2Ffiles%2FGeoServer%2F2.7.1.1%2F&ts=1438140277 -o geoserver.zip
    # mkdir /usr/share/geoserver
    # # chown `whoami`:`whoami` /usr/share/geoserver
    # unzip geoserver.zip -d /usr/share/geoserver
    # # add GEOSERVER_HOME env var for us and geoserver
    # echo " " >> /home/eresearch/.profile
    # echo " " >> /home/geonetwork/.profile
    # echo "export GEOSERVER_HOME=/usr/share/geoserver/geoserver-2.7.1.1" >> /home/eresearch/.profile
    # echo "export GEOSERVER_HOME=/usr/share/geoserver/geoserver-2.7.1.1" >> /home/geonetwork/.profile

    # # -- get postgres and postgis -----
    # add-apt-repository -y ppa:ubuntugis/ubuntugis-unstable
    # apt-get -y -q update
    # apt-get -y -q install postgresql postgresql-client postgresql-contrib postgis

    # # -- set up postgres / postgis -----
    # # eresearch superuser
    # sudo -u postgres -- createuser -s eresearch
    # # make a geoserver user, and db, and get it ready to GIS
    # sudo -u eresearch -- createuser geoserver
    # sudo -u eresearch -- createdb geoserver
    # sudo -u eresearch -- psql -d geoserver -c 'create extension postgis;'

  SHELL
end
