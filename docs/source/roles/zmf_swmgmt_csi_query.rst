
:github_url: https://github.com/IBM/ibm_zosmf/tree/master/plugins/roles/zmf_swmgmt_csi_query

.. _zmf_swmgmt_csi_query_module:


zmf_swmgmt_csi_query -- Query a SMP/E CSI data set
==================================================


.. contents::
   :local:
   :depth: 1


Synopsis
--------
- The \ :strong:`IBM z/OSMF collection`\  provides an Ansible role, referred to as \ :strong:`zmf\_swmgmt\_csi\_query`\ , to query a SMP/E global zone CSI data set directly or to query the CSI associated with a software instance.







Variables
---------


 

zmf_host
  Hostname of the z/OSMF server, specified in the inventory file or as an argument on the playbook command.


  | **required**: True
  | **type**: str


 

zmf_port
  Port number of the z/OSMF server. If z/OSMF is not using the default port, you need to specify a value for this parameter in the inventory file or as an argument on the playbook command.


  | **required**: False
  | **type**: str
  | **default**: 443


 

zmf_user
  User ID for authenticating with the z/OSMF server.

  This variable can be specified in the inventory file or as an argument on the playbook command.


  | **required**: True
  | **type**: str


 

zmf_password
  Password to be used for authenticating with z/OSMF server.

  This variable can be specified in the inventory file or as an argument on the playbook command.


  | **required**: True
  | **type**: str


 

software_instance_name
  Name of the software instance.

  A software instance name must be specified when a software instance UUID or a CSI data set name are not specified. If a software instance UUID is specified in addition to a software instance and system nickname, then the software instance UUID is used by default.


  This variable can be specified in the inventory file or as an argument on the playbook command.


  | **required**: False
  | **type**: str


 

system_nickname
  Nickname of the z/OSMF host system that has access to the volumes and data sets where the software instance resides.


  A system nickname name must be specified when a software instance UUID or a CSI data set name are not specified. If a software instance UUID is specified in addition to a software instance and system nickname, then the software instance UUID is used by default.


  This variable can be specified in the inventory file or as an argument on the playbook command.


  | **required**: False
  | **type**: str


 

software_instance_uuid
  A UUID of a software instance. A UUID is assigned to every software instance and can be obtained using the "List the software instances defined to z/OSMF" REST API.


  A UUID can also be obtained using the zmf\_swmgmt\_zos\_system\_uuid Ansible role which retrieves the UUID for the software instance that represents the installed software for the specified z/OSMF host system.


  A software instance UUID name must be specified when a software instance or a CSI data set name are not specified. If a software instance or a CSI data set name are specified, then the software instance UUID is used by default.


  This variable can be specified in the inventory file or as an argument on the playbook command.


  | **required**: False
  | **type**: str


 

csi_data_set_name
  A global zone CSI data set to query when it is not associated with a defined software instance object.


  A CSI data set name must be specified when a software instance or a software instance UUID are not specified. If a software instance UUID is specified in addition to a CSI data set name, then the software instance UUID is used by default.


  This variable can be specified in the inventory file or as an argument on the playbook command.


  | **required**: False
  | **type**: str


 

zones
  The list of zones to be queried. You may provide one or more specific zone names, or any of these values:


  GLOBAL (To query the global zone)


  ALLTZONES (To query all target zones)


  ALLDZONES (To query all DLIB zones)


  \* (To query the global zone and all zones defined in the global zone's ZONEINDEX)


  Zone names are accepted in mixed case and are folded to uppercase automatically. This list variable needs to be in following format: \ :literal:`'"GLOBAL","ALLTZONES","ALLDZONES"'`\ 


  This variable can be specified in the inventory file or as an argument on the playbook command.


  | **required**: True
  | **type**: arr


 

entries
  The list of entry types to be queried. You may provide one or more entry types, or asterisk ('\*') can be used to indicate all entry types will be queried. Entry types are accepted in mixed case and are folded to uppercase automatically.


  Refer to https://www.ibm.com/docs/en/zos/3.1.0?topic=command-valid-entry-types for the list of valid types.


  This variable can be specified in the inventory file or as an argument on the playbook command.


  | **required**: True
  | **type**: arr


 

subentries
  The list of subentry types to be returned. You may provide one or more subentry types, or asterisk ('\*') can be used to indicate all subentry types will be returned. Subentry types are accepted in mixed case and are folded to uppercase automatically. If no subentries are provided, then only the entry name and zone will be returned for matching entries.


  Refer to https://www.ibm.com/docs/en/zos/3.1.0?topic=command-valid-subentry-types for the list of valid types.


  This variable can be specified in the inventory file or as an argument on the playbook command.


  | **required**: False
  | **type**: arr


 

filter
  The list of conditions with which to limit the entries to be returned. A condition is in the form: subentry operator 'value' For example, FMID = 'HP10230' or INSTALLDATE \>= '23203'. The subentry type of a filter condition is accepted in mixed case and is folded to uppercase automatically. The value of a filter condition is case sensitive and is not folded to uppercase. If a filter is not provided then all entries of the specified type in the specified zones will be returned.


  Refer to https://www.ibm.com/docs/en/zos/3.1.0?topic=command-filter-parameter-syntax for a detailed description of the syntax for the filter.


  This variable can be specified in the inventory file or as an argument on the playbook command.


  | **required**: False
  | **type**: str


 

csi_query_response_file
  The path to the file that will contain the results from the csi query operation.

  The directory must already exist otherwise there will be an error writing the results to the file. If the file exists in the directory already, it will be overwritten by the new response when the playbook is executed. If the file doesn't exist in the directory, it will be created.


  This variable can be specified in the inventory file or as an argument on the playbook command.


  | **required**: True
  | **type**: str


 

remote_zmf_user
  User ID for authenticating with a remote z/OSMF server.  Used only if the csi data set resides on a remote z/OSMF server.


  | **required**: False
  | **type**: str


 

remote_zmf_password
  Password for authenticating with a remote z/OSMF server.

  | **required**: False
  | **type**: str


 

proxy_zmf_user
  User ID for authenticating with an HTTP proxy server.

  | **required**: False
  | **type**: str


 

proxy_zmf_password
  Password for authenticating with an HTTP proxy server.

  | **required**: False
  | **type**: str




Examples
--------

.. code-block:: yaml+jinja

   
   - name: sample of querying a CSI data set
     hosts: sampleHost
     gather_facts: no
     collections:
       - ibm.ibm_zosmf

     tasks:
       - include_role :
           name: zmf_swmgmt_csi_query




Notes
-----

.. note::
   - The given example assumes you have an inventory file \ :emphasis:`inventory.yml`\  that contains the values for the variables described above, such as z/OSMF host server, userid, password, software instance name and system, and response file name.


   - Command syntax to call a playbook using an inventory file: \ :literal:`ansible-playbook -i inventory software\_management\_csi\_query\_CICDtest1.yml`\ 


   - Command syntax to call a playbook using command arguments: \ :literal:`ansible-playbook software\_management\_csi\_query\_CICDtest1.yml -e zmf\_user=zosmf\*\* -e zmf\_password=zosmf\*\*`\ 


   - When the role is executed, a message shown in following example is displayed, \ :literal:`"msg": "Output filename= /tmp/xxx/csi\_query\_response.json"`\ . This message includes a file path and file name where the csi query information for the requested software instance is returned.








