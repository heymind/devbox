FROM ubuntu:17.04

# ENV APT_MIRROR="mirrors.163.com"
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8 

   

# RUN if [ $APT_MIRROR ] ; then \
#     sed -i 's/archive.ubuntu.com/'$APT_MIRROR'/g' /etc/apt/sources.list; fi

RUN apt-get update \
    && apt-get install -y  locales dialog apt-utils software-properties-common 

# Set the locale
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen
 

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs

RUN apt-get install -y python-pip python3-pip

RUN add-apt-repository ppa:neovim-ppa/stable \
    && apt-get update \
    && apt-get install -y neovim

RUN pip3 install neovim

RUN apt-get install -y git wget curl cmake tmux zsh openssh-server sudo

RUN mkdir /var/run/sshd
RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

RUN useradd -m -s /usr/bin/zsh -G sudo box \
    && echo "box:box" | chpasswd

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

