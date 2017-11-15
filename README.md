LLDP role
=========

This role facilitates the configuration of link layer discovery protocol (LLDP) attributes at a global and interface level. It supports the configuration of hello, mode, multiplier, advertise tlvs, management interface, FCoE, ISCSI at global and interface level. This role is abstracted for dellos9 and dellos10.

The LLDP role requires an SSH connection for connectivity to a Dell EMC Networking device. You can use any of the built-in Dell EMC Networking OS connection variables, or the *provider* dictionary.

Installation
------------

    ansible-galaxy install Dell-Networking.dellos-lldp

Role variables
--------------

- Role is abstracted using the *ansible_net_os_name* variable that can take dellos9 and dellos10 values
- If *dellos_cfg_generate* is set to true, the variable generates the role configuration commands in a file
- Any role variable with a corresponding state variable set to absent negates the configuration of that variable
- Setting an empty value for any variable negates the corresponding configuration
- Variables and values are case-sensitive

**dellos_lldp keys**

| Key        | Type                      | Description                                             | Support               |
|------------|---------------------------|---------------------------------------------------------|-----------------------|
| ``global_lldp_state`` | string: absent,present   | Removes LLDP at a global level if set to absent | dellos9 |
| ``enable``  | boolean         | Enables or disables LLDP at a global level | dellos9, dellos10 |
| ``hello`` | integer | Configures the global LLDP hello interval (5 to 180) | dellos9 |
| ``mode``  | string: rx,tx   | Configures global LLDP mode configuration | dellos9 |
| ``multiplier`` | integer | Configures the global LLDP multiplier (2 to 10) | dellos9, dellos10 |
| `` reinit `` | integer | Configures the reinit value (1-10) | dellos10 |
| `` timer`` | integer | Configures the timer value (5-254) | dellos10 |
| ``fcoe_priority_bits`` | integer | Configures priority bits for FCoE traffic (1 to FF) |  dellos9 |
| ``iscsi_priority_bits`` | integer | Configures priority bits for ISCSI traffic (1 to FF) | dellos9 |
| ``dcbx`` | dictionary  | Configures DCBx parameters at the global level (see ``dcbx.*``)     |  dellos9 |
| ``dcbx.version`` | string     | Configures DCBx version | dellos9 |
| ``advertise`` | dictionary     | Configures TLV advertisement at the global level (see ``advertise.*``)    | dellos9, dellos10 |
| ``advertise.dcbx_tlv`` | string     | Configures DCBx TLVs advertisements | dellos9 |
| ``advertise.dcbx_tlv_state`` | string: present,absent     | Deleletes DCBx TLVs advertisement if set to absent | dellos9 |
| ``advertise.dcbx_appln_tlv`` | string     | Configures DCBx application priority TLVs advertisement | dellos9 |
| ``advertise.dcbx_appln_tlv_state`` | string: present,absent     | Deletes DCBx application priority TLVs advertisement if set to absent | dellos9 |
| ``advertise.dot1_tlv`` | dictionary     | Configures 802.1 TLVs advertisement (see ``dot1_tlv.*``) | dellos9 |
| ``dot1_tlv.port_tlv`` | dictionary     | Configures 802.1 TLVs advertisement (see ``port_tlv.*``) | dellos9 |
| ``port_tlv.protocol_vlan_id`` | boolean     | Configures 802.1 VLAN ID TLVs advertisement | dellos9 |
| ``port_tlv.port_vlan_id`` | boolean     | Configures 802.1 VLAN ID TLVs advertisement | dellos9 |
| ``dot1_tlv.vlan_tlv`` | dictionary     | Configures 802.1 VLAN TLVs advertisement (see ``vlan_tlv.*``) |  dellos9 |
| ``vlan_tlv.vlan_range`` | string     | Configures 802.1 VLAN name TLVs advertisement | dellos9 |
| ``advertise.dot3_tlv`` | dictionary     | Configures 802.3 TLVs advertisement (see ``dot3_tlv.*``) | dellos9 |
| ``dot3_tlv.max_frame_size`` | boolean     | Configures 802.3 maximum frame size TLVs advertisement | dellos9 |
| ``advertise.port_descriptor`` | boolean     | Configures global port descriptor advertisement | dellos9 |
| ``advertise.management_tlv`` | string     | Configures global management TLVs advertisement | dellos9 |
| ``advertise.management_tlv_state`` | string: absent,present     | Deletes global TLVs advertisement if set to absent | dellos9 |
| ``advertise.med`` | dictionary     | Configures MED TLVs advertisement (see ``med_tlv.*``) | dellos9, dellos10 |
| ``med.global_med`` | boolean     | Configures global MED TLVs advertisement | dellos9 |
| ``med.fast_start_repeat_count`` | integer | Configures med fast start repeat count value on OS10 devices. | dellos10 |
| ``med.application`` | list     | Configures global MED TLVs advertisement for the application (see ``application.*``) | dellos9, dellos10 |
| ``application.name`` | string     | Configures the application name for MED TLVs advertisement | dellos9, dellos10 |
| ``application.vlan_id`` | integer     | Configures the VLAN ID for the application MED TLVs advertisement (1 to 4094) | dellos9, dellos10 |
| ``application.priority_tagged`` | boolean     | Configures priority tagged for the application MED TLVs advertisement; mutually exclusive with *application.vlan_id* | dellos9 |
| ``application.l2_priority`` | integer     | Configures the L2 priority for the application MED TLVs advertisement (0 to 7) | dellos9, dellos10 | 
| ``application.code_point_value`` | integer     | Configures differentiated services code point values for MED TLVs advertisement (0 to 63) | dellos9, dellos10 |
| ``application.vlan_type`` | string: tag, untag | Configures vlan type for the application MED TLvs advertisemnet | dellos10 |
| ``application.network_policy_id`` | integer | Configures network policy id for the application MED TLVs advertisemnet | dellos10 | 
| ``application.state`` | string, choices: present*, absent | Removes the application if set to absent. | dellos10 |
| ``med.location_identification`` | list     | Configures MED location identification TLVs advertisement (see ``location_identification.*``) | dellos9 |
| ``location_identification.loc_info`` | string     | Configures location information for MED TLVs advertisement | dellos9 |
| ``location_identification.value`` | string     | Configures location information values | dellos9 |
| ``location_identification.state`` | string: absent,present   | Deletes the location information if set to absent | dellos9 |
| ``management_interface`` | dictionary     | Configures LLDP on the management interface (see ``management_interface.*``)     | dellos9 |
| ``management_interface.enable``  | boolean         | Enables or disables LLDP on the management interface | dellos9 |
| ``management_interface.hello`` | integer | Configures LLDP hello interval on the management interface (5 to 180) | dellos9 |
| ``management_interface.mode``  | string: rx,tx   | Configures LLDP mode on the management interface | dellos9 |
| ``management_interface.multiplier`` | integer | Configures LLDP multiplier on the management interface (2 to 10) | dellos9 |
| ``management_interface.advertise`` | dictionary     | Configures TLV advertisement on the management interface (see ``advertise.*``)     | dellos9 |
| ``advertise.port_descriptor`` | boolean     | Configures port descriptor advertisement on the management interface  | dellos9 |
| ``advertise.management_tlv`` | string     | Configures management TLVs advertisement  | dellos9 |
| ``advertise.management_tlv_state`` | string: absent,present     | Deletes management TLVs advertisement if set to absent | dellos9 |
| ``local_interface`` | dictionary     | Configures LLDP at the interface level (see ``local_interface.*``)     |  dellos9, dellos10 |
| ``local_interface.<interface name>`` | dictionary     | Configures LLDP at the interface level (see ``<interface name>.*``)     | dellos9, dellos10 |
| ``<interface name>.state`` | string: absent,present   | Removes LLDP at the interface level if set to absent | dellos9 |
|  ``<interface name>.enable``  | boolean         | Enables or disables LLDP at the interface level | dellos9 |
| ``<interface name>.hello`` | integer | Configures LLDP hello interval at the interface level (5 to 180) | dellos9 |
| ``<interface name>.mode``  | string: rx,tx   | Configures LLDP mode configuration at the interface level | dellos9, dellos10 |
| ``<interface name>.state`` | string, choices: absent, present   | Configures transmit/receive at the interface level.| dellos10 |
| ``<interface name>.multiplier`` | integer | Configures LLDP multiplier at the interface level (2 to 10) |  dellos9 |
| ``<interface name>.dcbx`` | dictionary  | Configures DCBx parameters at the interface level (see ``dcbx.*``)     | dellos9 |
| ``dcbx.version`` | string     | Configures DCBx version at the interface level  | dellos9 |
| ``dcbx.port_role`` | string     | Configures DCBx port role at the interface level  | dellos9 |
| ``<interface name>.advertise`` | dictionary     | Configures TLV advertisement at the interface level (see ``advertise.*``)     | dellos9, dellos10 |
| ``advertise.dcbx_tlv`` | string     | Configures DCBx TLVs advertisement at the interface level | dellos9 |
| ``advertise.dcbx_tlv_state`` | string: present,absent     | Deletes interface level DCBx TLVs advertisement if set to absent | dellos9 |
| ``advertise.dcbx_appln_tlv`` | string     | Configures DCBx application priority TLVs advertisement at the interface level |  dellos9 |
| ``advertise.dcbx_appln_tlv_state`` | string: present,absent     | Deletes interface level DCBx application priority TLVs advertisement if set to absent | dellos9 |
| ``advertise.dot1_tlv`` | dictionary     | Configures 802.1 TLVs advertisement at the interface level (see ``dot1_tlv.*``) | dellos9 |
| ``dot1_tlv.port_tlv`` | dictionary     | Configures 802.1 TLVs advertisement at the interface level (see ``port_tlv.*``) | dellos9 |
| ``port_tlv.protocol_vlan_id`` | boolean     | Configures 802.1 VLAN ID TLVs advertisement at the interface level | dellos9 |
| ``port_tlv.port_vlan_id`` | boolean     | Configures 802.1 VLAN ID TLVs advertisement at the interface level | dellos9 | 
| ``dot1_tlv.vlan_tlv`` | dictionary     | Configures 802.1 VLAN TLVs advertisement at the interface level (see ``vlan_tlv.*``) | dellos9 |
| ``vlan_tlv.vlan_range`` | string     | Configures 802.1 VLAN name TLVs advertisement at the interface level | dellos9  |
| ``advertise.dot3_tlv`` | dictionary     | Configures 802.3 TLVs advertisement at the interface level (see ``dot3_tlv.*``) | dellos9 |
| ``dot3_tlv.max_frame_size`` | boolean   | Configures 802.3 maximum frame size TLVs advertisement at the interface level | dellos9 |
| ``advertise.port_descriptor`` | boolean     | Configures port descriptor advertisement at the interface level | dellos9 |
| ``advertise.management_tlv`` | string     | Configures TLVs advertisement at the interface level | dellos9 | 
| ``advertise.management_tlv_state`` | string: absent,present     | Deletes TLVs advertisement at the interface level if set to absent | dellos9 |
| ``advertise.med`` | dictionary     | Configures MED TLVs advertisement at the interface level (see ``med_tlv.*``) | dellos9, dellos10 |
| ``med.enable`` | boolean     | Enables interface level med capabilities.| dellos10 |
| ``med.tlv`` | string | Configures med TLV advertisement at interface level.| dellos10 |
| ``med.tlv_state`` | string, choices: present*, absent | Removes the interface level MED configuration if set to absent. |dellos10 |
| ``med.global_med`` | boolean     | Configures MED TLVs advertisement at the interface level | dellos9 |
| ``med.application`` | list     | Configures MED TLVs advertisement for the application at the interface level (see ``application.*``) | dellos9, dellos10 |
| ``application.network_policy_id`` | integer    | Configures the network_policy_id for the application of med.| dellos10 |
| ``application.state`` | string, choices: present*, absent | Removes the associated network policy id for the application if set to absent.| dellos10 |
| ``application.name`` | string     | Configures the application name for MED TLVs advertisement | dellos9 |
| ``application.vlan_id`` | integer     | Configures the VLAN ID for the application MED TLVs advertisement at the interface level (1 to 4094) | dellos9 |
| ``application.priority_tagged`` | boolean     | Configures priority tagged for the application MED TLVs advertisement at the interface level; mutually exclusive with *application.vlan_id* | dellos9 |
| ``application.l2_priority`` | integer     | Configures the L2 priority for the application MED TLVs advertisement at the interface level (0 to 7) | dellos9 |
| ``application.code_point_value`` | integer     | Configures differentiated services code point value for MED TLVs advertisement at the interface level (0 to 63) | dellos9 |
| ``med.location_identification`` | list     | Configures MED location identification TLVs advertisement at the interface level (see ``location_identification.*``) | dellos9 |
| ``location_identification.loc_info`` | string     | Configures location information for MED TLVs advertisement at the interface level | dellos9 |
| ``location_identification.value`` | string     | Configures the location information value for MED TLVs advertisement at the interface level | dellos9 |
| ``location_identification.state`` | string: absent,present   | Deletes the interface level MED location information if set to absent | dellos9 |
| ``advertise.tlv`` | list    | Configures TLVs advertisement at interface level. See the following &lt;interface_name&gt;.tlv.* for each list item.  | dellos10 |
| ``tlv.name`` | string, choices: basic-tlv, dcbxp, dcbxp-appln, dot1-tlv, dot3-tlv  | Configures corresponding to the tlv name specified at the interface.| dellos10 |
| ``tlv.value`` | string     | Specifies corresponding tlv value according to the name as a string.| dellos10 |
| ``tlv.state`` | choices: present*, absent   | Removes the interface level TLVs advertisement if set to absent.| dellos10 |


Connection variables
--------------------

Ansible Dell EMC Networking roles require connection information to establish communication with the nodes in your inventory. This information can exist in the Ansible *group_vars* or *host_vars* directories, or in the playbook itself.

| Key         | Required | Choices    | Description                                         |
|-------------|----------|------------|-----------------------------------------------------|
| ``host`` | yes      |            | Specifies the hostname or address for connecting to the remote device over the specified transport |
| ``port`` | no       |            | Specifies the port used to build the connection to the remote device; if unspecified, the value defaults to 22 |
| ``username`` | no       |            | Specifies the username that authenticates the CLI login to connect to the remote device; if value is unspecified, the ANSIBLE_NET_USERNAME environment variable value is used  |
| ``password`` | no       |            | Specifies the password that authenticates the connection to the remote device; if value is unspecified, the ANSIBLE_NET_PASSWORD environment variable value is used  |
| ``authorize`` | no       | yes, no\*   | Instructs the module to enter privileged mode on the remote device before sending any commands; if value is unspecified, the ANSIBLE_NET_AUTHORIZE environment variable value is used, and the device attempts to execute all commands in non-privileged mode |
| ``auth_pass`` | no       |            | Specifies the password to use if required to enter privileged mode on the remote device; if *authorize* is set to no, this key is not applicable, and the ANSIBLE_NET_AUTH_PASS environment variable value is used  |
| ``provider`` | no       |            | Passes all connection arguments as a dictionary object; all constraints (such as required or choices) must be met either by individual arguments or values in this dictionary |

> **NOTE**: Asterisk (\*) denotes the default value if none is specified.

Dependencies
------------

The *dellos-lldp* role is built on modules included in the core Ansible code. These modules were added in Ansible version 2.2.0.

Example playbook
----------------

This example uses the *dellos-lldp* role to configure protocol lldp. It creates a *hosts* file with the switch details and corresponding variables. The hosts file should define the *ansible_net_os_name* variable with corresponding Dell EMC networking OS name. When *dellos_cfg_generate* is set to true, the variable generates the configuration commands as a .part file in *build_dir* path. By default, the variable is set to false. It writes a simple playbook that only references the *dellos-lldp* role.

**Sample hosts file**

    leaf1 ansible_host= <ip_address> ansible_net_os_name= <OS name(dellos9)>

**Sample host_vars/leaf1**

    hostname: leaf1
    provider:
      host: "{{ hostname }}"
      username: XXXX
      password: XXXX
      authorize: yes
      auth_pass: XXXX
    build_dir: ../temp/dellos9
    dellos_lldp:
       global_lldp_state: present
       enable: false
        mode: rx
       multiplier: 3
       fcoe_priority_bits: 3
       iscsi_priority_bits: 3
       hello: 6
       dcbx:
         version: auto
       management_interface:
         hello: 7
         multiplier: 3
         mode: tx
         enable: true
         advertise:
           port_descriptor: false
           management_tlv: management-address system-capabilities
           management_tlv_state: absent
       advertise:
         dcbx_tlv: pfc
         dcbx_tlv_state: absent
         dcbx_appln_tlv: fcoe
         dcbx_appln_tlv_state:
         dot1_tlv:
           port_tlv:
              protocol_vlan_id: true
              port_vlan_id: true
           vlan_tlv:
              vlan_range: 2-4
         dot3_tlv:
           max_frame_size: false
         port_descriptor: false
         management_tlv: management-address system-capabilities
         management_tlv_state: absent
         med:
           global_med: true
           application:
             - name: "guest-voice"
               vlan_id: 2
               l2_priority: 3
               code_point_value: 4
             - name: voice
               priority_tagged: true
               l2_priority: 3
               code_point_value: 4
           location_identification:
             - loc_info: ecs-elin
               value: 12345678911
               state: present
       local_interface:
         fortyGigE 1/3:
           lldp_state: present
           enable: false
           mode: rx
           multiplier: 3
           hello: 8
           dcbx:
             version: auto
             port_role: auto-upstream
           advertise:
             dcbx_tlv: pfc
             dcbx_tlv_state: present
             dcbx_appln_tlv: fcoe
             dcbx_appln_tlv_state: absent
             dot1_tlv:
               port_tlv:
                 protocol_vlan_id: true
                 port_vlan_id: true
               vlan_tlv:
                 vlan_range: 2-4
                 state: present
             dot3_tlv:
               max_frame_size: true
             port_descriptor: true
             management_tlv: management-address system-capabilities
             management_tlv_state: absent
             med:
               application:
                 - name: guest-voice
                   vlan_id: 2
                   l2_priority: 3
                   code_point_value: 4
                 - name: voice
                   priority_tagged: true
                   l2_priority: 3
                   code_point_value: 4
               location_identification:
                 - loc_info: ecs-elin
                   value: 12345678911

**Simple playbook to setup system - leaf.yaml**

    - hosts: leaf1
      roles:
         - Dell-Networking.dellos-lldp

**Run**

    ansible-playbook -i hosts leaf.yaml

(c) 2017 Dell EMC
