FROM wrenchproject/wrench:1.10

MAINTAINER Henri Casanova <henric@hawaii.edu>

USER root

# update repository list
RUN apt-get update

# install compiler (likely installed already though)
RUN apt-get -y install g++ gcc

# set timezone
RUN echo "America/Los_Angeles" > /etc/timezone && export DEBIAN_FRONTEND=noninteractive && apt-get install -y tzdata

# install basic things, just in case
RUN apt-get -y install vim pkg-config git cmake cmake-data wget sudo curl zip

# clone and install the scheduling_with_simulations_simulator with the right commit tab
RUN git clone https://github.com/wrench-project/scheduling_using_simulation_simulator.git && cd scheduling_using_simulation_simulator && git checkout b58de28b66d80df91d1a57855acf967f2c4b7c81 &&  mkdir build && cd build && cmake .. && make -j4 && sudo make install && cd ../.. && /bin/rm -rf scheduling_using_simulation_simulator/

# install mongo
RUN apt-get -y install gnupg
RUN wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | apt-key add -
RUN echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-5.0.list
RUN apt-get update
RUN apt-get install -y mongodb-org

# install pip
RUN wget https://bootstrap.pypa.io/get-pip.py && python3 get-pip.py && /bin/rm get-pip.py

# install pymongo
RUN python3 -m pip install pymongo

# install matplotlib
RUN python3 -m pip install matplotlib

#################################################
# Non-root user 'me'
#################################################

RUN useradd -ms /bin/bash me 
RUN adduser me sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER me
WORKDIR /home/me

#RUN /bin/rm -rfi ./examples 
RUN echo "Clone the jsspp2022_submission_data repo: git clone https://github.com/wrench-project/jsspp2022_submission_data.git" > /home/me/README
RUN echo "And follow the instructions in the README at https://github.com/wrench-project/jsspp2022_submission_data" >> /home/me/README
