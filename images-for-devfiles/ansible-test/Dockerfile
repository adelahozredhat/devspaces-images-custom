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
RUN pip install setuptools_rust wheel ansible ansible-builder ansible-runner ansible-navigator 