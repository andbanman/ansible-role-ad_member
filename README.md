# ansible-role-ad_member

Join a Linux host to an Active Directory domain as a domain member.

Configuring identity mapping between AD users/groups and Unix UID/GIGs is often the most difficult part of joining linux to AD. The two mapping options are winbind and sssd, where sssd is preferred since it does not require a local database and is consistent accross hosts. Starting with Samba 4.8.0, winbind must be installed to connect to AD; strictly speaking this only affects hosts that serve samba file shares, while other hosts can continue to use sssd for system authentication (pam, nss, etc). As such, this role does not permit a working Samba server.

To join a Linux Samba server to an AD domain, see role ansible-role-ad_member_samba.

## Requirements

A working AD domain with DNS and DHCP properly configured. In particular, this config does not specfiy the domain controller host(s) and so they must be discoverable over the network. See REQUIRED variables below to configure the role.

## Variables
```
# REQUIRED
ad_member_domain           # e.g. "my.domain"
ad_member_workgroup        # e.g. "MYDOMAIN"
ad_member_kerberos_user    # user capable of joining host to domain
ad_member_kerberos_pass    # SECRET user password, should be kept in an encrypted vault.
                           # no_log is used to prevent exposing the secret.

# OPTIONAL
ad_member_test_user        # user name to test join was successful
ad_member_test_user_uid    # user id to test

# ... see defaults/ for other variables for advanced usage
```
