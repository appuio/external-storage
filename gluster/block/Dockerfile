FROM centos:7

MAINTAINER APPUiO Maintainer

ENV CGO_ENABLED=0
ADD gluster/block/gluster-block.repo /etc/yum.repos.d
ADD gluster/block /go/src/github.com/kubernetes-incubator/external-storage/gluster/block
ADD vendor /go/src/github.com/kubernetes-incubator/external-storage/vendor
ADD lib /go/src/github.com/kubernetes-incubator/external-storage/lib

RUN yum update -y && \
    yum install -y gluster-block && \
    export GOPATH=/go && \
    yum -y install golang-bin && \
    go install github.com/kubernetes-incubator/external-storage/gluster/block/cmd/glusterblock-provisioner && \
    yum -y history undo last && \
    yum clean all

USER 1001

ENTRYPOINT ["/go/bin/glusterblock-provisioner"]
