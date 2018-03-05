acm_cert
=========

Handle certificates in AWS ACM.

Take a acm_certs as a list of dict decsribing certificate properties then
import it to aws.

Currently there is no ansible module to handle it yet so as a quick
implementation I use the aws cli. It is desirable to make new ansible acm_cert
using boto3 to handle the acm certs operations. <TODO>

See here for mroe info.
https://docs.aws.amazon.com/cli/latest/reference/acm/import-certificate.html

Requirements
------------

aws cli on the run host

Role Variables
--------------

acm_certs - a list of dict decsribing certificate properties

Examples:
```
acm_certs:
    - name: CertName
      domain_name: "examples.com"
      certificate: "/path/to/cert/file"
      private-key: "/path/to/private/key"
      certificate-chain: "/path/to/cert/chain"
      certificate-arn: "/existing/cert/arn/to/be/update"
```
- field `certificate-arn` is optional if not provided then new certificate will be imported.
- field `certificate-chain` is also optional
- The `private-key` must point to unencrypted private key. You can encrypt using ansible vault though.
- Field 'name' will be added to the tag 'Name' in ACM
- It will create new or update the ACM cert with domain_name matched.

Dependencies
------------


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
