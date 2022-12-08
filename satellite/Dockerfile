FROM registry.redhat.io/ubi8/ubi:latest

LABEL maintainer="DevTeam" \
      com.redhat.component="ubi8-container" \
      name="ubi8" \ 
      com.redhat.license_terms="https://www.redhat.com/en/about/red-hat-end-user-license-agreements#UBI" \ 
      summary="Provides the latest release of Red Hat Universal Base Image 8." \ 
      description="The Universal Base Image is designed and engineered to be the base layer for all of your containerized applications, middleware and utilities. This base image is freely redistributable, but Red Hat only supports Red Hat technologies through subscriptions for Red Hat products. This image is maintained by Red Hat and updated regularly." \ 
      io.k8s.display-name="Red Hat Universal Base Image 8" \ 
      io.openshift.expose-services="" \ 
      io.openshift.tags="base rhel8"

COPY ENTITLE.pem /etc/pki/entitlement/ENTITLEMENT.pem
COPY ENTITLEMENT-key.pem /etc/pki/entitlement/ENTITLEMENT-key.pem

RUN rm -rf /var/log/* && mkdir -p /var/log/rhsm && dnf clean all && rm -rf /var/cache/dnf && echo -e '\
[caas_RedHat_UBI_8_ubi-8-appstream]\n\
metadata_expire = 1\n\
enabled_metadata = 1\n\
sslclientcert = /etc/pki/entitlement/ENTITLEMENT.pem\n\
baseurl = https://satellite.example.com/pulp/repos/caas/Library/ubi-8/custom/RedHat_UBI_8/ubi-8-appstream\n\
sslverify = 1\n\
name = ubi-8-appstream\n\
sslclientkey = /etc/pki/entitlement/ENTITLEMENT-key.pem\n\
enabled = 1\n\
sslcacert = /etc/rhsm-host/ca/katello-server-ca.pem\n\
gpgcheck = 0\n\
\n\
[caas_RedHat_UBI_8_ubi-8-baseos]\n\
metadata_expire = 1\n\
enabled_metadata = 1\n\
sslclientcert = /etc/pki/entitlement/ENTITLEMENT.pem\n\
baseurl = https://satellite.example.com/pulp/repos/caas/Library/ubi-8/custom/RedHat_UBI_8/ubi-8-baseos\n\
sslverify = 1\n\
name = ubi-8-baseos\n\
sslclientkey = /etc/pki/entitlement/ENTITLEMENT-key.pem\n\
enabled = 1\n\
sslcacert = /etc/rhsm-host/ca/katello-server-ca.pem\n\
gpgcheck = 0\n\
\n\
[caas_RedHat_UBI_8_ubi-8-codeready-builder]\n\
metadata_expire = 1\n\
enabled_metadata = 1\n\
sslclientcert = /etc/pki/entitlement/ENTITLEMENT.pem\n\
baseurl = https://satellite.example.com/pulp/repos/caas/Library/ubi-8/custom/RedHat_UBI_8/ubi-8-codeready-builder\n\
sslverify = 1\n\
name = ubi-8-codeready-builder\n\
sslclientkey = /etc/pki/entitlement/ENTITLEMENT-key.pem\n\
enabled = 1\n\
sslcacert = /etc/rhsm-host/ca/katello-server-ca.pem\n\
gpgcheck = 0\n\
' >  /etc/yum.repos.d/ubi.repo 

CMD ["/bin/bash"]
