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

ADD https://mirror.openshift.com/pub/openshift-v4/clients/ocp/stable-4.8/openshift-client-linux.tar.gz /tmp/
ADD https://storage.googleapis.com/kubernetes-release/release/v1.18.6/bin/linux/amd64/kubectl /tmp/
ADD https://github.com/argoproj/argo-cd/releases/download/v2.1.3/argocd-linux-amd64 /tmp/
ADD https://github.com/mikefarah/yq/releases/download/v4.19.1/yq_linux_amd64 /tmp/
ADD https://github.com/stedolan/jq/releases/download/jq-1.6/jq-linux64 /tmp/

RUN tar xzvf /tmp/openshift-client-linux.tar.gz \
  && make -C /tmp/openshift-client-linux \
  && rm /tmp/openshift-client-linux.tar.gz

RUN yum -y -q update
RUN pip install --upgrade pip



CMD tail -f /dev/null

# append Brew metadata here
ENV SUMMARY="Red Hat CodeReady Workspaces - WorkAthon enviroment for Gramola" \
    DESCRIPTION="Red Hat CodeReady Workspaces - WorkAthon enviroment for Gramola" \
    PRODNAME="codeready-workspaces" \
    COMPNAME="workathon-gramola"

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