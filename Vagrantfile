# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.provider "virtualbox" do |vb|
    # Customize the amount of memory on the VM:
    vb.memory = 8*1024
    vb.cpus   =  4
  end
  #
  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    yum update -y
    yum install -y redhat-lsb-core yum-utils deltarpm
    yum groupinstall -y "Development Tools"
    yum install -y \
        asciidoc \
        autoconf \
        automake \
        bzip2-devel \
        fontconfig-devel \
        freetype-devel \
        gcc \
        gcc-c++ \
        gdbm-devel \
        glibc-devel \
        glibc-devel.i686 \
        libX11-devel \
        libXext-devel \
        libXft-devel \
        libXi-devel \
        libXmu-devel \
        libXpm-devel \
        libXrender-devel \
        libXt-devel \
        libcurl-devel \
        libgcc \
        libgcc.i686 \
        libjpeg-turbo-devel \
        libpng-devel \
        libstdc++-devel \
        libstdc++.i686 \
        libtool \
        mesa-libGL-devel \
        mesa-libGLU-devel \
        ncurses-devel \
        openldap-devel \
        openssl-devel \
        perl-DBD-SQLite \
        perl-ExtUtils-MakeMaker \
        readline-devel \
        subversion \
        swig \
        tcl-devel \
        texinfo \
        tk-devel \
        xmlto \
        zlib-devel

    yum install -y libevent-devel
    mkdir /tmp/build
    cd /tmp/build
    wget https://github.com/tmux/tmux/releases/download/2.7/tmux-2.7.tar.gz
    tar -xf tmux-2.7.tar.gz
    cd tmux-2.7
    LDFLAGS="-L/usr/local/lib -Wl,-rpath=/usr/local/lib" ./configure --prefix=/usr/local
    make
    make install
    cd
    rm -rf /tmp/build

    yum install -y vim

    mkdir -p /usr/local/bin
    curl https://beyondgrep.com/ack-2.24-single-file > /usr/local/bin/ack && chmod 0755 /usr/local/bin/ack

  SHELL
  config.vm.synced_folder "output/", "/output"
end
