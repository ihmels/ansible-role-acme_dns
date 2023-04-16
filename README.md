acme_dns
========

Install and configure [acme-dns](https://github.com/joohoi/acme-dns/).

Requirements
------------

None.

Role Variables
--------------

The default values for the variables are set in [defaults/main.yml](defaults/main.yml)

```yaml
---
# The version to install
acme_dns_version: "1.0"

# Service user configuration
acme_dns_home_dir: "/var/lib/acme-dns"
acme_dns_user: acme-dns
acme_dns_group: acme-dns

# "error", "warning", "info" or "debug"
acme_dns_log_level: debug

# Disable registration endpoint
acme_dns_disable_registration: false

# TLS configuration
# 
# Use "letsencrypt" (or "letsencryptstaging" for testing) to automatically issue a certificate:
# acme_dns_tls = "letsencrypt"
# acme_dns_acme_email: "admin@example.org"
#
# Or use "cert" to use your own certificate:
# acme_dns_tls = "cert"
# acme_dns_tls_cert_privkey: "/path/to/private_key"
# acme_dns_tls_cert_fullchain: "/path/to/certificate"
#
# Use "none" to use no certificate.
acme_dns_tls: "none"
acme_dns_tls_cert_privkey: null
acme_dns_tls_cert_fullchain: null
acme_dns_acme_email: ""

# DNS server configuration
acme_dns_domain: auth.example.org
acme_dns_admin: hostmaster.example.org
acme_dns_public_ipv4: "{{ ansible_default_ipv4.address | default(ansible_all_ipv4_addresses[0]) }}"
acme_dns_public_ipv6: "{{ ansible_default_ipv6.address | default(ansible_all_ipv6_addresses[0]) }}"
```

Dependencies
------------

None.

Example Playbook
----------------

```yaml
---
- hosts: servers
  roles:
    - role: ihmels.acme_dns
      vars:
        acme_dns_domain: auth.example.org
        acme_dns_public_ipv4: "192.0.2.0"
        acme_dns_public_ipv6: "2001:db8::"
        acme_dns_tls: "letsencryptstaging"
        acme_dns_acme_email: "admin@example.org"
```

License
-------

MIT
