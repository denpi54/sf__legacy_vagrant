Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"
  config.vm.hostname = "pg84"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 1
  end

  config.vm.network "private_network", type: "dhcp"

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt update
    sudo apt install -y build-essential libreadline-dev zlib1g-dev flex bison wget

    cd /home/vagrant
    wget https://ftp.postgresql.org/pub/source/v8.4.22/postgresql-8.4.22.tar.gz
    tar -xvzf postgresql-8.4.22.tar.gz
    cd postgresql-8.4.22

    ./configure --prefix=/usr/local/pgsql
    make
    sudo make install

    sudo adduser postgres --disabled-password --gecos ""
    sudo mkdir /usr/local/pgsql/data
    sudo chown postgres /usr/local/pgsql/data
    sudo -u postgres /usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
    sudo -u postgres /usr/local/pgsql/bin/pg_ctl -D /usr/local/pgsql/data -l logfile start
  SHELL
end

