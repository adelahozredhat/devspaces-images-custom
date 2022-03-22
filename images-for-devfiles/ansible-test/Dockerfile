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
FROM registry.access.redhat.com/ubi8/python-38:1-80 as builder
USER 0


RUN yum -y -q update
RUN yum install -y -q curl vim policycoreutils python3-policycoreutils yum-utils
RUN pip install setuptools_rust wheel ansible ansible-builder ansible-runner ansible-navigator ansible-test

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