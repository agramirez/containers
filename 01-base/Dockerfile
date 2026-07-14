FROM debian:trixie

# update and upgrade
RUN apt-get update && apt-get upgrade -y

# install the basics
RUN apt-get install -y git
RUN apt-get install -y build-essential
RUN apt-get install -y libssl-dev

# install opam and rocq dependencies
RUN apt-get install -y linux-libc-dev
RUN apt-get install -y m4
RUN apt-get install -y opam
RUN apt-get install -y time
RUN apt-get install -y zip
RUN apt-get install -y zsh
RUN apt-get install -y libgmp3-dev
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y pkg-config

# install web stuff
RUN apt-get install -y curl
RUN apt-get install -y wget
RUN apt-get install -y lynx

# now we install documentation tools
RUN apt-get install -y default-jdk
RUN apt-get install -y graphviz

# setup latex
RUN apt-get install -y texlive-full 

# for additional security we install sudo and user devuser
ARG USERNAME=devuser
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN apt-get install -y sudo
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME --shell /bin/zsh \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

COPY hack.sh /tmp/hack.sh
RUN chmod +x /tmp/hack.sh
RUN /tmp/hack.sh
COPY .zshrc /home/$USERNAME/
USER $USERNAME

# setup opam and rocq
RUN opam init -y --disable-sandboxing --compiler=5.3.0
RUN opam switch 5.3.0
RUN opam install -y num
RUN opam repo add -y coq-released https://coq.inria.fr/opam/released
RUN opam pin add -y coq 9.0.0
RUN opam install -y coq-simple-io
RUN opam install -y vscoq-language-server
RUN opam update -y
RUN opam upgrade -y
RUN eval `opam config env`
