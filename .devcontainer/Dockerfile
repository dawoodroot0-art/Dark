FROM tutum/metasploitable

# ആവശ്യമായ ടൂളുകളും SSH സർവീസും ഉറപ്പാക്കാൻ
RUN apt-get update && apt-get install -y \
    openssh-server \
    sudo \
    git \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir /var/run/sshd

# ഡിഫോൾട്ട് ക്രെഡൻഷ്യൽസ് (msfadmin:msfadmin)
RUN echo 'root:root' | chpasswd

EXPOSE 22 80 21 445 3306

CMD ["/usr/sbin/sshd", "-D"]
