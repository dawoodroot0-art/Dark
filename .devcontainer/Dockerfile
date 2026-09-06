FROM tleemcgrath/metasploitable2

# ആവശ്യമായ SSH സർവീസ്, സുഡോ, പാസ്‌വേഡ് പാക്കേജുകൾ ഉറപ്പാക്കുന്നു
RUN apt-get update && apt-get install -y \
    openssh-server \
    sudo \
    git \
    curl \
    passwd \
    procps \
    && rm -rf /var/lib/apt/lists/*

# SSH ഡയറക്ടറി സെറ്റ് ചെയ്യുന്നു
RUN mkdir -p /var/run/sshd

# നോർമൽ യൂസർ (devuser) ഉണ്ടാക്കി പെർമിഷൻ നൽകുന്നു (Password: devpass)
RUN useradd -ms /bin/bash devuser && \
    echo "devuser:devpass" | chpasswd && \
    echo "devuser ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# റൂട്ട് യൂസർ പാസ്‌വേഡ് സെറ്റ് ചെയ്യുന്നു (Password: rootpass അല്ലെങ്കിൽ msfadmin)
RUN echo "root:rootpass" | chpasswd

# SSH ലോഗിൻ പെർമിഷൻ ശരിയാക്കുന്നു
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's/session    required     pam_loginuid.so/session optional pam_loginuid.so/' /etc/pam.d/sshd

EXPOSE 22 21 80 443 445 3306

CMD ["/usr/sbin/sshd", "-D"]
