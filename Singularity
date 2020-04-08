Bootstrap: shub
From: willgpaik/centos7_aci

%environment
    source /opt/rh/devtoolset-8/enable

    export PETSC_DIR=/opt/sw/petsc
    export LIBMESH_DIR=/opt/sw/libmesh
    PATH="/usr/local/bin/:$PATH:/usr/lib64/openmpi/bin/:/opt/sw/libmesh/bin:/opt/sw/moose/python/peacock"
    LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/lib64/openmpi/lib/:/opt/sw/petsc/lib:/opt/sw/libmesh/lib"
    CPATH=$CPATH:/opt/sw/petsc/include:/opt/sw/libmesh/include
    MPI_ROOT=/usr/lib64/openmpi/
    export PATH
    export LD_LIBRARY_PATH
    export CPATH
    export MPI_ROOT
    export BOOST_ROOT=/usr/local/

%post
    yum install -y tcl \
            m4 \
            freeglut-devel \
            blas-devel \
            lapack-devel \
            libX11-devel \
            python3-devel \
            python3 \
            diffutils \
            wget \
            which \
            boost-devel \
            bison \
            flex \
            tar

    source /opt/rh/devtoolset-8/enable

    PATH="/usr/local/bin/:$PATH:/usr/lib64/openmpi/bin/"
    LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/lib64/openmpi/lib/"
    MPI_ROOT=/usr/lib64/openmpi/
    export PATH
    export LD_LIBRARY_PATH
    export MPI_ROOT
    export BOOST_ROOT=/usr/local/

    mkdir -p /opt/sw/moose
    mkdir -p /opt/sw/petsc
    mkdir -p /opt/sw/libmesh

    export CC=mpicc
    export CXX=mpicxx
    export LIBMESH_DIR=/opt/sw/libmesh

    export MOOSE_JOBS=2
    
    cd /opt/sw
    git clone https://github.com/idaholab/moose.git
    cd moose
    git checkout master
    git clone https://gitlab.com/petsc/petsc.git
    PETSC_PREFIX=/opt/sw/petsc ./scripts/update_and_rebuild_petsc.sh
    rm -rf petsc
    export PETSC_DIR=/opt/sw/petsc

    git clone https://github.com/libMesh/libmesh.git
    cd libmesh
    git submodule update --init
    cd ..
    ./scripts/update_and_rebuild_libmesh.sh
    rm -rf libmesh

    # Make symbolic link for invoking Python
    ln -sf /usr/bin/python3 /usr/bin/python

    pip3 install PyQt5
