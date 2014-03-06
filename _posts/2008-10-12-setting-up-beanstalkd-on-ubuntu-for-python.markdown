---
layout: parand
title:  "Setting Up Beanstalkd on Ubuntu for Python"
date:   2008-10-12 10:00:00
categories: say/index.php
---
[beanstalkd](http://xph.us/software/beanstalkd/) is a promising in-memory queuing system in the mold of memcached \(minimal configuration, just works\) with client libraries in a variety of languages. The following worked for me for installing it on Ubuntu 8.04:
    
    
    mkdir ~/packages
    
    # pre-requisite: libevent.
    cd ~/packages
    wget http://monkey.org/~provos/libevent-1.4.8-stable.tar.gz
    tar zxvf http://monkey.org/~provos/libevent-1.4.8-stable.tar.gz
    cd libevent-1.4.8-stable
    ./configure
    make
    sudo make install
    
    # add /usr/local/lib to your load library path so beanstalkd can find libevent
    vi ~/.bashrc   (add the following somewhere near the end):
    export LD_LIBRARY_PATH=$LD_LIBRYARY_PATH:/usr/local/lib
    
    (exit vi)
    source ~/.bashrc
    
    # need git in order to get latest code for beanstalkd
    cd ~/packages
    sudo apt-get install git-core
    
    # grab beanstalkd
    git clone http://xph.us/src/beanstalkd.git
    cd beanstalkd
    make
    
    # now you should be able to start the beanstalkd daemon
    ./beanstalkd -d -p 99988
    
    # get the python beanstalkd client
    cd ~/packages
    svn checkout http://pybeanstalk.googlecode.com/svn/trunk/ pybeanstalk-read-only
    
    cd pybeanstalk-read-only
    sudo python setup.py install
    
    # get pyyaml, a pre-requisite for the python beanstalkd client
    cd ~/packages
    wget http://pyyaml.org/download/pyyaml/PyYAML-3.06.tar.gz
    tar zxvf PyYAML-3.06.tar.gz
    cd PyYAML-3.06
    sudo python setup.py install
    
    # open two different shells (or use screen) type the following in the two different shells:
    cd ~/packages/pybeanstalk-read-only/examples
    python simple_clients.py producer localhost 99988
    python simple_clients.py consumer localhost 99988
    
    
