- [1 管理指南](README.md)


- [2 管理概述](020-ji-qun-cao-zuo.md)


- [3 集群性能监控](030-ji-qun-jian-kong.md)


- [4 扩容和缩容](040-ji-qun-kuo-rong.md)

- [5 备份](045-ji-qun-bei-fen.md)

- [6 排查系统问题](050-pai-cha-xi-tong-wen-ti.md)


- [7 系统目录参考](060-system-catalog-ref/README.md)
    - [7.1 系统表](060-system-catalog-ref/010-xi-tong-biao.md)
    - [7.2 系统视图](060-system-catalog-ref/020-xi-tong-shi-tu.md)
    - [7.3 系统目录定义](060-system-catalog-ref/030-system-catalog-define/README.md)
        - [7.3.1 gp_configuration_history](060-system-catalog-ref/030-system-catalog-define/gpconfiguration-history.md)
        - [7.3.2 gp_db_interfaces](060-system-catalog-ref/030-system-catalog-define/gpdb-interfaces.md)
        - [7.3.3 gp_distributed_log](060-system-catalog-ref/030-system-catalog-define/gpdistributed-log.md)
        - [7.3.4 gp_distributed_xacts](060-system-catalog-ref/030-system-catalog-define/gpdistributed-xacts.md)
        - [7.3.5 gp_distribution_policy](060-system-catalog-ref/030-system-catalog-define/gpdistribution-policy.md)
        - [7.3.6 gpexpand.expansion_progress](060-system-catalog-ref/030-system-catalog-define/gpexpandexpansionprogress.md)
        - [7.3.7 gpexpand.status](060-system-catalog-ref/030-system-catalog-define/gpexpandstatus.md)
        - [7.3.8 gpexpand.status_detail](060-system-catalog-ref/030-system-catalog-define/gpexpandstatusdetail.md)
        - [7.3.9 gp_fastsequence](060-system-catalog-ref/030-system-catalog-define/gpfastsequence.md)
        - [7.3.10 gp_fault_strategy](060-system-catalog-ref/030-system-catalog-define/gpfault-strategy.md)
        - [7.3.11 gp_global_sequence](060-system-catalog-ref/030-system-catalog-define/gpglobal-sequence.md)
        - [7.3.12 gp_id](060-system-catalog-ref/030-system-catalog-define/gpid.md)
        - [7.3.13 gp_interfaces](060-system-catalog-ref/030-system-catalog-define/gpinterfaces.md)
        - [7.3.14 gp_persistent_database_node](060-system-catalog-ref/030-system-catalog-define/gppersistent-database-node.md)
        - [7.3.15 gp_persistent_filespace_node](060-system-catalog-ref/030-system-catalog-define/gppersistent-filespace-node.md)
        - [7.3.16 gp_persistent_relation_node](060-system-catalog-ref/030-system-catalog-define/gppersistent-relation-node.md)
        - [7.3.17 gp_persistent_tablespace_node](060-system-catalog-ref/030-system-catalog-define/gppersistent-tablespace-node.md)
        - [7.3.18 gp](060-system-catalog-ref/030-system-catalog-define/gppgdatabase.md)
        - [7.3.19 gp_relation_node](060-system-catalog-ref/030-system-catalog-define/gprelation-node.md)
        - [7.3.20 gp_resqueue_status](060-system-catalog-ref/030-system-catalog-define/gpresqueue-status.md)
        - [7.3.21 gp_segment_configuration](060-system-catalog-ref/030-system-catalog-define/gpsegment-configuration.md)
        - [7.3.22 gp_transaction_log](060-system-catalog-ref/030-system-catalog-define/gptransaction-log.md)
        - [7.3.23 gp_version_at_initdb](060-system-catalog-ref/030-system-catalog-define/gpversion-at-initdb.md)
        - [7.3.24 pg](060-system-catalog-ref/030-system-catalog-define/pgaggregate.md)
        - [7.3.25 pg](060-system-catalog-ref/030-system-catalog-define/pgam.md)
        - [7.3.26 pg_amop](060-system-catalog-ref/030-system-catalog-define/pgamop.md)
        - [7.3.27 pg_amproc](060-system-catalog-ref/030-system-catalog-define/pgamproc.md)
        - [7.3.28 pg_appendonly](060-system-catalog-ref/030-system-catalog-define/pgappendonly.md)
        - [7.3.29 pg_attrdef](060-system-catalog-ref/030-system-catalog-define/pgattrdef.md)
        - [7.3.30 pg_attribute_encoding](060-system-catalog-ref/030-system-catalog-define/pgattribute-encoding.md)
        - [7.3.31 pg_attribute](060-system-catalog-ref/030-system-catalog-define/pgattribute.md)
        - [7.3.32 pg_auth_members](060-system-catalog-ref/030-system-catalog-define/pgauth-members.md)
        - [7.3.33 pg_authid](060-system-catalog-ref/030-system-catalog-define/pgauthid.md)
        - [7.3.34 pg_available_extension_versions](060-system-catalog-ref/030-system-catalog-define/pgavailable-extension-versions.md)
        - [7.3.35 pg_available_extensions](060-system-catalog-ref/030-system-catalog-define/pgavailable-extensions.md)
        - [7.3.36 pg_cast](060-system-catalog-ref/030-system-catalog-define/pgcast.md)
        - [7.3.37 pg_class](060-system-catalog-ref/030-system-catalog-define/pgclass.md)
        - [7.3.38 pg_compression](060-system-catalog-ref/030-system-catalog-define/pgcompression.md)
        - [7.3.39 pg_constraint](060-system-catalog-ref/030-system-catalog-define/pgconstraint.md)
        - [7.3.40 pg_conversion](060-system-catalog-ref/030-system-catalog-define/pgconversion.md)
        - [7.3.41 pg_database](060-system-catalog-ref/030-system-catalog-define/pgdatabase.md)
        - [7.3.42 pg_depend](060-system-catalog-ref/030-system-catalog-define/pgdepend.md)
        - [7.3.43 pg_description](060-system-catalog-ref/030-system-catalog-define/pgdescription.md)
        - [7.3.44 pg_enum](060-system-catalog-ref/030-system-catalog-define/pgenum.md)
        - [7.3.45 pg_extension](060-system-catalog-ref/030-system-catalog-define/pgextension.md)
        - [7.3.46 pg_exttable](060-system-catalog-ref/030-system-catalog-define/pgexttable.md)
        - [7.3.47 pg_filespace_entry](060-system-catalog-ref/030-system-catalog-define/pgfilespace-entry.md)
        - [7.3.48 pg_filespace](060-system-catalog-ref/030-system-catalog-define/pgfilespace.md)
        - [7.3.49 pg_index](060-system-catalog-ref/030-system-catalog-define/pgindex.md)
        - [7.3.50 pg_inherits](060-system-catalog-ref/030-system-catalog-define/pginherits.md)
        - [7.3.51 pg_language](060-system-catalog-ref/030-system-catalog-define/pglanguage.md)
        - [7.3.52 pg_largeobject](060-system-catalog-ref/030-system-catalog-define/pglargeobject.md)
        - [7.3.53 pg_listener](060-system-catalog-ref/030-system-catalog-define/pglistener.md)
        - [7.3.54 pg_locks](060-system-catalog-ref/030-system-catalog-define/pglocks.md)
        - [7.3.55 pg_max_external_files](060-system-catalog-ref/030-system-catalog-define/pgmax-external-files.md)
        - [7.3.56 pg](060-system-catalog-ref/030-system-catalog-define/pgnamespace.md)
        - [7.3.57 pg_opclass](060-system-catalog-ref/030-system-catalog-define/pgopclass.md)
        - [7.3.58 pg_operator](060-system-catalog-ref/030-system-catalog-define/pgoperator.md)
        - [7.3.59 pg_partition_columns](060-system-catalog-ref/030-system-catalog-define/pgpartition-columns.md)
        - [7.3.60 pg_partition_encoding](060-system-catalog-ref/030-system-catalog-define/pgpartition-encoding.md)
        - [7.3.61 pg_partition_rule](060-system-catalog-ref/030-system-catalog-define/pgpartition-rule.md)
        - [7.3.62 pg_partition_templates](060-system-catalog-ref/030-system-catalog-define/pgpartition-templates.md)
        - [7.3.63 pg_partition](060-system-catalog-ref/030-system-catalog-define/pgpartition.md)
        - [7.3.64 pg_partitions](060-system-catalog-ref/030-system-catalog-define/pgpartitions.md)
        - [7.3.65 pg_pltemplate](060-system-catalog-ref/030-system-catalog-define/pgpltemplate.md)
        - [7.3.66 pg_proc](060-system-catalog-ref/030-system-catalog-define/pgproc.md)
        - [7.3.67 pg_resourcetype](060-system-catalog-ref/030-system-catalog-define/pgresourcetype.md)
        - [7.3.68 pg_resqueue_attributes](060-system-catalog-ref/030-system-catalog-define/pgresqueue-attributes.md)
        - [7.3.69 pg_resqueue](060-system-catalog-ref/030-system-catalog-define/pgresqueue.md)
        - [7.3.70 pg_resqueuecapability](060-system-catalog-ref/030-system-catalog-define/pgresqueuecapability.md)
        - [7.3.71 pg_rewrite](060-system-catalog-ref/030-system-catalog-define/pgrewrite.md)
        - [7.3.72 pg](060-system-catalog-ref/030-system-catalog-define/pgroles.md)
        - [7.3.73 pg_shdepend](060-system-catalog-ref/030-system-catalog-define/pgshdepend.md)
        - [7.3.74 pg](060-system-catalog-ref/030-system-catalog-define/pgshdescription.md)
        - [7.3.75 pg_stat_activity](060-system-catalog-ref/030-system-catalog-define/pgstat-activity.md)
        - [7.3.76 pg_stat_last_operation](060-system-catalog-ref/030-system-catalog-define/pgstat-last-operation.md)
        - [7.3.77 pg_stat_last_shoperation](060-system-catalog-ref/030-system-catalog-define/pgstat-last-shoperation.md)
        - [7.3.78 pg_stat_operations](060-system-catalog-ref/030-system-catalog-define/pgstat-operations.md)
        - [7.3.79 pg_stat_partition_operations](060-system-catalog-ref/030-system-catalog-define/pgstat-partition-operations.md)
        - [7.3.80 pg_stat_replication](060-system-catalog-ref/030-system-catalog-define/pgstat-replication.md)
        - [7.3.81 pg_stat_resqueues](060-system-catalog-ref/030-system-catalog-define/pgstat-resqueues.md)
        - [7.3.82 pg](060-system-catalog-ref/030-system-catalog-define/pgstatistic.md)
        - [7.3.83 pg](060-system-catalog-ref/030-system-catalog-define/pgtablespace.md)
        - [7.3.84 pg_trigger](060-system-catalog-ref/030-system-catalog-define/pgtrigger.md)
        - [7.3.85 pg_type_encoding](060-system-catalog-ref/030-system-catalog-define/pgtype-encoding.md)
        - [7.3.86 pg_type](060-system-catalog-ref/030-system-catalog-define/pgtype.md)
        - [7.3.87 pg_user_mapping](060-system-catalog-ref/030-system-catalog-define/pguser-mapping.md)
        - [7.3.88 pg_window](060-system-catalog-ref/030-system-catalog-define/pgwindow.md)


- [8 gp_toolkit 管理方案](070-gptoolkit-admin-plan.md)


- [9 gpperfmon 数据库](080-gpperfmon-database/README.md)
    - [9.1 database_*](080-gpperfmon-database/database.md)
    - [9.2 diskspace_*](080-gpperfmon-database/diskspace.md)
    - [9.3 dynamic_memory_info](080-gpperfmon-database/dynamicmemory-info.md)
    - [9.4 filerep_*](080-gpperfmon-database/filerep.md)
    - [9.5 interface_stats_](080-gpperfmon-database/interfacestats.md)
    - [9.6 log_alert_*](080-gpperfmon-database/logalert.md)
    - [9.7 memory](080-gpperfmon-database/memoryinfo.md)
    - [9.8 queries_*](080-gpperfmon-database/queries.md)
    - [9.9 segment_*](080-gpperfmon-database/segment.md)
    - [9.10 system_*](080-gpperfmon-database/system.md)



