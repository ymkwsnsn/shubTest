Bootstrap: yum
OSVersion: 7
MirrorURL: http://mirror.centos.org/centos-%{OSVERSION}/%{OSVERSION}/os/$basearch/
Include: yum

%help

%setup

%files

%labels

%environment
    export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

%post
    echo "Installing Development Tools YUM group"
    yum -y groupinstall "Development Tools"
    echo "Installing OFED Infiniband Support"
    yum -y install libibverbs-devel
    yum -y install infiniband-diags perftest qperf opensm
    yum -y groupinstall "Infiniband Support"
    echo "Installing OpenMPI into container..."
    yum -y install wget
    wget https://download.open-mpi.org/release/open-mpi/v3.1/openmpi-3.1.1.tar.gz
    tar -xvf openmpi-3.1.1.tar.gz
    cd openmpi-3.1.1
    ./configure --prefix=/usr/local --with-platform=contrib/platform/mellanox/optimized
    make all install
    /usr/local/bin/mpicc examples/ring_c.c -o /usr/bin/mpi_ring

#osu bench
     OSU_VERSION=5.4.2
     wget http://mvapich.cse.ohio-state.edu/download/mvapich/osu-micro-benchmarks-${OSU_VERSION}.tar.gz
     tar -xvf osu-micro-benchmarks-${OSU_VERSION}.tar.gz
     cd osu-micro-benchmarks-${OSU_VERSION}
     ./configure --prefix=/usr/local CC=/usr/local/bin/mpicc CXX=/usr/local/bin/mpicxx
     make
     make install
