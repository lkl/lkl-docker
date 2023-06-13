ARG IMAGE_NAME

# As of June 2023, freebsd pkg site, http://pkg.FreeBSD.org/FreeBSD:11:amd64/quarterly/
# is no longer available.  We currently have no plan to update FreeBSD support,
# so, we reuse existing image, from 0.4 tag, to create newer images.
# If we will update FreeBSD version of support, revert this commit and
# rewrite the relevant part of scripts.
FROM lkldocker/circleci-freebsd11-x86_64:0.4 AS freebsd
LABEL authors="Hajime Tazaki <thehajime@gmail.com>"

FROM $IMAGE_NAME
COPY --from=freebsd /freebsd /freebsd
COPY --from=freebsd /home/ubuntu /home/ubuntu
RUN sudo apt-get update && \
    sudo apt-get install -y wget xz-utils qemu-system-x86 p7zip-full build-essential m4 bison flex git vim file libtool automake autoconf autogen pkg-config && \
    sudo rm -rf /var/lib/apt/lists/*


ENV QEMU "qemu-system-x86_64 -m 2048 \
     -hda FreeBSD-11.1-RELEASE-amd64.qcow2 \
     -netdev user,id=mynet0,hostfwd=tcp:127.0.0.1:7722-:22 \
     -device e1000,netdev=mynet0 -display none -daemonize"

ENV MYSSH "/home/ubuntu/sshpass-1.06/sshpass -p password ssh \
    -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no \
    -q root@localhost -p7722"

ENV MYSCP "/home/ubuntu/sshpass-1.06/sshpass -p password scp \
    -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no -q"

ENV PATH /usr/lib/ccache/:/freebsd/bin:${PATH}

