FROM wrenchproject/wrench:1.10

MAINTAINER Henri Casanova <henric@hawaii.edu>

USER root

# update repository list
RUN apt-get update

# install compiler
RUN apt-get -y install g++ gcc

# set timezone
RUN echo "America/Los_Angeles" > /etc/timezone && export DEBIAN_FRONTEND=noninteractive && apt-get install -y tzdata

# install basic things, just in case
RUN apt-get -y install vim pkg-config git cmake cmake-data wget sudo curl zip
# install mongo (likely old version, but that's ok)
RUN apt-get -y install gnupg
RUN wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | apt-key add -
RUN echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-5.0.list
RUN apt-get update
RUN apt-get -y install -y mongodb-org

# clone and install the scheduling_with_simulations_simulator with the right commit tab
RUN git clone  https://github.com/wrench-project/scheduling_using_simulation_simulator.git && cd scheduling_using_simulation_simulator && git checkout 78a22933e7fd2beacc7efc802d46569e2044ea02 &&  mkdir build && cd build && cmake .. && make -j4 && sudo make install && cd ../.. && /bin/rm -rf scheduling_using_simulation_simulator/

# install pip
RUN wget https://bootstrap.pypa.io/get-pip.py && python3 get-pip.py && /bin/rm get-pip.py
# install pymongo
RUN python3 -m pip install pymongo
# install matplotlib
RUN python3 -m pip install matplotlib


#################################################
# WRENCH's user
#################################################

#RUN useradd -ms /bin/bash wrench 
#RUN adduser wrench sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER wrench
WORKDIR /home/wrench
ENV CXX="g++-9" CC="gcc-9"

RUN /bin/rm -r ./examples 
RUN echo "Clone the jsspp2022_submission_data repo: git clone https://github.com/wrench-project/jsspp2022_submision_data.git" > /home/wrench/README
