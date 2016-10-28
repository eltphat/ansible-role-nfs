NFS server/client Role 
=======================

Install NFS server/client. This role has been specifically developed to be used in the INDIGO project.

Role Variables
--------------

The variables that can be passed to this role and a brief description about them are as follows.

	# NFS install mode: server or client
	nfs_mode: server
	# Line to add to the /etc/exports file
	nfs_exports: [{path: "/home", export: "vnode*(rw,async,no_root_squash,no_subtree_check,insecure)"}]
	# Line to add to the /etc/exports file
	nfs_client_imports: [{ local: "/home", remote: "/home", server_host: "{{hostvars['server']['ansible_default_ipv4']}}" }]

Example Playbook
----------------

This an example of how to install a Torque/PBS cluster:

    - hosts: server
      roles:
      - { role: 'indigo-dc.nfs', nfs_mode: 'server', nfs_exports: [{path: "/home", export: "vnode*(fsid=0,rw,async,no_root_squash,no_subtree_check,insecure)"}] }

    - hosts: client
      roles:
      - { role: 'indigo-dc.nfs', nfs_mode: 'client', nfs_client_imports: [{ local: "/home", remote: "/home", server_host: "{{hostvars['server']['ansible_default_ipv4']}}" }] }

License
-------

Apache Licence v2 [1]

[1] http://www.apache.org/licenses/LICENSE-2.0
