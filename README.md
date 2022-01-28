# **NOTE:** Development and maintenance of this software has stopped.
For more information, see [DISCONTINUATION_NOTICE.md](DISCONTINUATION_NOTICE.md).
***

sap-netweaver-preconfigure-assert
================

This role checks if a RHEL 7 or RHEL 8 system has been set up according to applicable SAP notes so that SAP NetWeaver can be installed.

Requirements
------------

None.

Note
----

The role can check if enough swap space as per the prerequisite checker in sapinst has been configured on the managed node. Please check the SAP NetWeaver installation guide for swap space requirements.

Role Variables
--------------

### Ignore assert errors
If the following variable is set to `yes`, the role will not fail in case of any assert errors. It will only print out warnings. Default is `no`, meaning that the role will fail on each assertion error.
```yaml
sap_netweaver_preconfigure_assert_ignore_errors
```

### Fail if there is less than 20480 MB of swap space configured
If the following variable is set to `no`, the role will not fail if less than 20480 MB of swap space is configured. Default is `yes`.
```yaml
sap_netweaver_preconfigure_assert_fail_if_not_enough_swap_space_configured
```

Example Playbook
----------------

Here is a simple playbook which will check if your RHEL system is configured correctly for installation of SAP NetWeaver:

```yaml
---
    - hosts: all
      roles:
         - role: sap-preconfigure-assert
         - role: sap-netweaver-preconfigure-assert

...
```

For a compact output when running with variable `sap_netweaver_preconfigure_assert_ignore_errors` to `yes`, you may use:
```yaml
ansible-playbook -l remote_host sap-netweaver-assert.yml | awk '/SAP note/||/FAIL:/||/WARN/||/PASS:/{sub ("    \"msg\": ", ""); print}'

```

License
-------

GNU General Public License v3.0

Author Information
------------------

Bernd Finger
