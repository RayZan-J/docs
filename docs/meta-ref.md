# System Catalog Reference #
This reference describes the Greenplum Database system catalog tables and views. System tables prefixed with *gp_* relate to the parallel features of Greenplum Database. Tables prefixed with *pg_* are either standard PostgreSQL system catalog tables supported in Greenplum Database, or are related to features Greenplum that provides to enhance PostgreSQL for data warehousing workloads. Note that the global system catalog for Greenplum Database resides on the master instance.
## System Tables ##
## System Views ##
## System Catalogs Definitions  ##
### gp_configuration_history ###
### gp_db_interfaces ###
### gp_distributed_log ###
### gp_distributed_xacts ###
### gp_distribution_policy ###
### gpexpand.expansion_progress ###
### gpexpand.status ###
### gpexpand.status_detail ###
### gp_fastsequence ###
### gp_fault_strategy ###
### gp_global_sequence ###
### gp_id ###
### gp_interfaces ###
### gp_persistent_database_node ###
### gp_persistent_filespace_node ###
### gp_persistent_relation_node ###
### gp_persistent_tablespace_node ###
### gp_pgdatabase ###
### gp_relation_node ###
### gp_resqueue_status ###
### gp_san_configuration ###
### gp_segment_configuration ###
### gp_transaction_log ###
### gp_version_at_initdb ###
### pg_aggregate ###
### pg_am ###
### pg_amop ###
### pg_amproc ###
### pg_appendonly ###
### pg_attrdef ###
### pg_attribute ###
### pg_attribute_encoding ###
### pg_auth_members ###
### pg_authid ###
### pg_cast ###
### pg_class ###
### pg_compression ###
### pg_constraint ###
### pg_conversion ###
### pg_database ###
### pg_depend ###
### pg_description ###
### pg_exttable ###
### pg_filespace ###
### pg_filespace_entry ###
### pg_index ###
### pg_inherits ###
### pg_language ###
### pg_largeobject ###
### pg_listener ###
### pg_locks ###
### pg_namespace ###
### pg_opclass ###
### pg_operator ###
### pg_partition ###
### pg_partition_columns ###
### pg_partition_encoding ###
### pg_partition_rule ###
### pg_partition_templates ###
### pg_partitions ###
### pg_pltemplate ###
### pg_proc ###
### pg_resourcetype ###
### pg_resqueue ###
### pg_resqueue_attributes ###
### pg_resqueuecapability ###
### pg_rewrite ###
### pg_roles ###
### pg_shdepend ###
### pg_shdescription ###
### pg_stat_activity ###
### pg_stat_last_operation ###
### pg_stat_last_shoperation ###
### pg_stat_operations ###
### pg_stat_partition_operations ###
### pg_stat_replication ###
### pg_statistic ###
### pg_stat_resqueues ###
### pg_tablespace ###
### pg_trigger ###
### pg_type ###
### pg_type_encoding ###
### pg_user_mapping ###
### pg_window ###