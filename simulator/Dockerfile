FROM wrenchproject/wrench:1.10

MAINTAINER Henri Casanova <henric@hawaii.edu>

# update repository list
RUN apt-get update

# install compiler
RUN apt-get -y install g++ gcc

# set timezone
RUN echo "America/Los_Angeles" > /etc/timezone && export DEBIAN_FRONTEND=noninteractive && apt-get install -y tzdata

# install basic things, just in case
RUN apt-get -y install vim pkg-config git cmake cmake-data wget sudo curl zip
# install mongo (likely old version, but that's ok)
RUN apt-get -y install mongodb-org

# clone and install the scheduling_with_simulations_simulator with the right commit tab
RUN git clone git@github.com:wrench-project/scheduling_using_simulation_simulator.git && cd scheduling_using_simulation_simulator.git && git checkout XXXXXX &&  mkdir build && cd build && cmake .. && make -j4 && sudo make install && cd ../.. && /bin/rm -rf scheduling_using_simulation_simulator.git

#################################################
# WRENCH's user
#################################################

RUN useradd -ms /bin/bash wrench 
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN adduser wrench sudo

USER wrench
WORKDIR /home/wrench
ENV CXX="g++-9" CC="gcc-9"

RUN echo "Clone the jsspp2022_submission_data repo" > /home/wrench/README
