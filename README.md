# Ansible Collection - redhat.jcliff

## About

This Ansible Collection wraps a tool called [JCliff](), designed to integrate the Java EE server [JBoss Enterprise Application (EAP)]() or its upstream counterpart [Wildfly]() into a configuration management tool such as Ansible.

## Install

### Installing the collection

To install this Ansible collection simply download the latest tarball and run the following command:

    $ ansible-galaxy collection install /path/to/redhat.jcliff.tgz

Alternatively, you can simply build the tarball (to then install it):

    $ ansible-galaxy collection build


### Ensuring JCliff is available

The collection itself only provides the integration of JCliff into Ansible. The tool needs to be installed and available on the system Ansible is running on. Refers to [JCliff]() for more information on how to install the tool manually.

For commodity purpose, the Collection comes with a role 'jcliff' to have Ansible install 'jcliff'. However, currently, this role **only** supports Linux distribution using Yum (namely Fedora, RHEL and CentOS):

    - hosts: ...
      collections:
        - redhat.jcliff
      roles:
        - jcliff
      vars:
        - ansible_distribution: Fedora
      tasks:
        ...

## Using the JCliff collection within your playbook

Once the Collection has been installed and JCliff is available on the system, you can directly use the tool within your playbook to configure a EAP or Wildfly instance:

    ---
    - hosts: localhost
      gather_facts: false
      collections:
        - redhat_middleware.jcliff

      tasks:

        - jcliff:
            wfly_home: /home/rpelisse/Repositories/redhat/ansible-jcliff-workspace/jboss-eap-7.2
            subsystems:
              - system_props:
                  - name: jcliff.enabled
                    value: 'enabled'
                  - name: jcliff.version
                    value: '1.0'

