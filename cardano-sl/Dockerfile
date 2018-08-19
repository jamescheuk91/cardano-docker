FROM debian:jessie

RUN apt-get update &&\
   apt-get install -y git curl bzip2 nginx sudo nano

RUN useradd -ms /bin/bash cardano &&\
   mkdir -m 0755 /nix &&\
   chown cardano /nix &&\
   mkdir -p /etc/nix &&\
   echo binary-caches = https://cache.nixos.org https://hydra.iohk.io > /etc/nix/nix.conf &&\
   echo binary-cache-public-keys = hydra.iohk.io:f/Ea+s+dFdN+3Y/G+FDgSq+a5NEWhJGzdjvKNGv0/EQ= >> /etc/nix/nix.conf &&\
   su - cardano -c 'git clone https://github.com/input-output-hk/cardano-sl.git /home/cardano/cardano-sl'

ADD nginx.conf /etc/nginx/conf.d/

USER cardano
ENV USER cardano
RUN curl https://nixos.org/nix/install | sh
WORKDIR /home/cardano/cardano-sl 
RUN git checkout tags/1.3.0

RUN . /home/cardano/.nix-profile/etc/profile.d/nix.sh && \
    nix-build --attr connectScripts.mainnet.wallet --out-link connect-to-mainnet -v 

CMD sudo /usr/sbin/service nginx restart && echo "Docker container ::: Nginx service restarted" & /home/cardano/cardano-sl/connect-to-mainnet