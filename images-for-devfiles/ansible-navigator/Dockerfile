FROM registry.redhat.io/ubi8/ubi:8.5
LABEL maintainer="Red Hat, Inc."

LABEL com.redhat.component="podman-container"
LABEL com.redhat.license_terms="https://www.redhat.com/en/about/red-hat-end-user-license-agreements#UBI"
LABEL name="rhel8/podman"
LABEL version="8.5"

LABEL License="ASL 2.0"

#labels for container catalog
LABEL summary="Manage Pods, Containers and Container Images"
LABEL description="podman (Pod Manager) is a fully featured container engine that is a simple daemonless tool. podman provides a Docker-CLI comparable command line that eases the transition from other container engines and allows the management of pods, containers and images.  Simply put: alias docker=podman.  Most podman commands can be run as a regular user, without requiring additional privileges. podman uses Buildah(1) internally to create container images. Both tools share image (not container) storage, hence each can use or manipulate images (but not containers) created by the other."
LABEL io.k8s.display-name="Podman"
LABEL io.openshift.expose-services=""

# Don't include container-selinux and remove
# directories used by yum that are just taking
# up space.
RUN dnf -y module enable container-tools:rhel8; dnf -y update; rpm --restore --quiet shadow-utils; \
dnf -y install crun podman fuse-overlayfs /etc/containers/storage.conf --exclude container-selinux; \
rm -rf /var/cache /var/log/dnf* /var/log/yum.*

RUN dnf install -y -q curl vim python3 policycoreutils python3-policycoreutils yum-utils
RUN pip3 install setuptools==45.2.0 ansible-navigator==1.1.0 ansible-builder==1.0.1

RUN chmod a+rwx /
RUN mkdir /.local
RUN chmod a+rwx /.local
RUN mkdir /.cache
RUN chmod a+rwx /.cache
RUN mkdir /.config
RUN chmod a+rwx /.config
RUN chmod a+rwx /usr/bin/newgidmap
RUN chmod a+rwx /usr/bin/newuidmap
RUN chmod a+rwx /usr/bin/fuse-overlayfs


RUN useradd podman
RUN echo podman:10000:5000 > /etc/subuid; \
echo podman:10000:5000 > /etc/subgid;

# RUN echo 1000660000:10000:5000 >> /etc/subuid; \
# echo 1000660000:10000:5000 >> /etc/subgid;

# RUN echo 1000650000:10000:5000 >> /etc/subuid; \
# echo 1000650000:10000:5000 >> /etc/subgid;


# RUN echo 1000670000:10000:5000 >> /etc/subuid; \
# echo 1000670000:10000:5000 >> /etc/subgid;



# VOLUME /var/lib/containers
# RUN mkdir -p /home/podman/.local/share/containers
# RUN chown podman:podman -R /home/podman
# VOLUME /home/podman/.local/share/containers

# https://raw.githubusercontent.com/containers/libpod/master/contrib/podmanimage/stable/containers.conf
ADD containers.conf /etc/containers/containers.conf
# https://raw.githubusercontent.com/containers/libpod/master/contrib/podmanimage/stable/podman-containers.conf
ADD podman-containers.conf /home/podman/.config/containers/containers.conf

# chmod containers.conf and adjust storage.conf to enable Fuse storage.
RUN chmod 644 /etc/containers/containers.conf; sed -i -e 's|^#mount_program|mount_program|g' -e '/additionalimage.*/a "/var/lib/shared",' -e 's|^mountopt[[:space:]]*=.*$|mountopt = "nodev,fsync=0"|g' /etc/containers/storage.conf
RUN mkdir -p /var/lib/shared/overlay-images /var/lib/shared/overlay-layers /var/lib/shared/vfs-images /var/lib/shared/vfs-layers; touch /var/lib/shared/overlay-images/images.lock; touch /var/lib/shared/overlay-layers/layers.lock; touch /var/lib/shared/vfs-images/images.lock; touch /var/lib/shared/vfs-layers/layers.lock

ENV _CONTAINERS_USERNS_CONFIGURED=""

CMD tail -f /dev/null

# append Brew metadata here
ENV SUMMARY="Red Hat CodeReady Workspaces - OpenJDK 8 + Node 12 + Python 3.8 plugin container" \
    DESCRIPTION="Red Hat CodeReady Workspaces - OpenJDK 8 + Node 12 + Python 3.8 plugin container" \
    PRODNAME="codeready-workspaces" \
    COMPNAME="plugin-java8-rhel8"

LABEL summary="$SUMMARY" \
      description="$DESCRIPTION" \
      io.k8s.description="$DESCRIPTION" \
      io.k8s.display-name="$DESCRIPTION" \
      io.openshift.tags="$PRODNAME,$COMPNAME" \
      com.redhat.component="$PRODNAME-$COMPNAME-container" \
      name="$PRODNAME/$COMPNAME" \
      version="2.15" \
      license="EPLv2" \
      maintainer="Nick Boldt <nboldt@redhat.com>" \
      io.openshift.expose-services="" \
      usage=""