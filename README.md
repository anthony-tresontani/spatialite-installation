spatialite-installation-for-django
==================================

It took me quite a while to install spatialite due to some missing *for dummy* installation procedure.

Here is my try to provide extra hints how to do it.
Be ready to configure / make / sudo make install as we will do everything from source.

First you need GEOS installed:

    wget http://download.osgeo.org/geos/geos-3.3.5.tar.bz2
    bzip2 -d geos-3.3.5.tar.bz2
    tar xvf geos-3.3.5.tar
    cd geos-3.3.5
    ./configure
    make
    sudo make install
  
And Proj:

    wget http://download.osgeo.org/proj/proj-4.8.0.tar.gz
    gzip -d proj-4.8.0.tar
    tar xvf proj-4.8.0.tar
    cd proj-4.8.0.tar
    ./configure
    make
    sudo make install
    
Then ReadOSM:

    wget http://www.gaia-gis.it/gaia-sins/readosm-1.0.0a.tar.gz
    ... same again ...
    
Finally, you can download spatialite and install it:
    
    wget http://www.gaia-gis.it/gaia-sins/libspatialite-3.0.1.tar.gz
    ... same ...
    
That will build `spatialite` command

Then swap your default `sqlite3` for `spatialite` 

    cp spatialite /usr/bin/sqlite3
    
If you run your django tests now, you will get  "The pysqlite library does not support C extension loading."
To fix that, you should re-install pysqlite2 manually after editing setup.cfg:

    wget http://code.google.com/p/pysqlite/downloads/detail?name=pysqlite-2.6.2.tar.gz
    gzip -d pysqlite-2.6.2.tar.gz
    tar xvf pysqlite-2.6.2.tar
    cd pysqlite-2.6.2
    vi setup.cfg
    Remove define=SQLITE_OMIT_LOAD_EXTENSION
    python setup.py install
    
Now, your test should be able to run.
    

