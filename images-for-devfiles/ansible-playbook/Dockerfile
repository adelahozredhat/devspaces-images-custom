#
# Copyright (c) 2018-2022 Red Hat, Inc.
# This program and the accompanying materials are made
# available under the terms of the Eclipse Public License 2.0
# which is available at https://www.eclipse.org/legal/epl-2.0/
#
# SPDX-License-Identifier: EPL-2.0
#
# Contributors:
#   Red Hat, Inc. - initial API and implementation
#   IBM Corporation - implementation
#

# Builder: check meta.yamls and create index.json
# https://access.redhat.com/containers/?tab=tags#/registry.access.redhat.com/ubi8/python-38
FROM registry.redhat.io/rhel8/python-38 as builder
USER 0


RUN yum -y -q update
RUN yum install -y -q curl vim policycoreutils python3-policycoreutils yum-utils
RUN python3 -m venv myvirtual_venv
RUN chmod 0755 myvirtual_venv
RUN source myvirtual_venv/bin/activate
RUN python3 -m pip install --upgrade pip
RUN python3 -m pip install setuptools==45.2.0 ansible==5.3.0
RUN deactivate
RUN python3 -m venv myvirtual_venv2
RUN chmod 0755 myvirtual_venv2
RUN source myvirtual_venv2/bin/activate
RUN python3 -m pip install --upgrade pip
RUN python3 -m pip install setuptools==45.2.0 ansible==2.9.0
RUN deactivate
RUN python3 -m venv myvirtual_venv3
RUN chmod 0755 myvirtual_venv3
RUN source myvirtual_venv3/bin/activate
RUN python3 -m pip install --upgrade pip
RUN python3 -m pip install setuptools==45.2.0 ansible==5.3.0
RUN deactivate



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