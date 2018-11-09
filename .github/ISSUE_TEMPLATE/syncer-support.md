---
name: "syncer Support"
about: "Requesting support for syncer Tool"

---

## syncer Support

Please describe your problem here:

>
>
>

Additionally, please provide the following info before submitting your issue. Thanks!

1. Versions of the tools

    - [ ] syncer version (run `syncer -V`):

        ```
        Release Version: v1.0.0-32-g714b355
        Git Commit Hash: 714b355bd014c5f198994fbdb219244f7cc50976
        Git Branch: master
        UTC Build Time: 2018-09-06 09:52:18
        Go Version: go version go1.11 linux/amd64
        ```

    - [ ] TiDB cluster version (execute `SELECT tidb_version();` in a MySQL client):

        ```
       没有使用tidb，只是使用了syncer做生成库的定时备份，从阿里云mysql同步到本地mysql
       阿里云mysql版本：5.6.16-log
       本地mysql版本：5.6.27
        ```

    - [ ] How did you deploy syncer?

        ```
        参考：https://github.com/pingcap/docs-cn/blob/master/tools/syncer.md
        # 下载 tool 压缩包
          wget http://download.pingcap.org/tidb-enterprise-tools-latest-linux-amd64.tar.gz
        # 解压到安装目录
        # 使用mydumper和loader做一次全量同步
        # 根据全量同步配置syncer.meta
        # 配置config.toml
         # 启动syncer
            ./bin/syncer -config config.toml -log-file syncer.log -log-rotate day -L info &
        ```

    - [ ] Other interesting information (system version, hardware config, etc):

        >systen version
        ```
        uname -a
        Linux test-hadoop002 3.10.0-693.2.2.el7.x86_64 #1 SMP Tue Sep 12 22:26:13 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
        cat /etc/redhat-release 
        CentOS Linux release 7.4.1708 (Core)
        ```
        >hardware config
        ```
        free -m
        total        used        free      shared  buff/cache   available
        Mem:          32012        9548        9205           1       13259       22014
        Swap:             0           0
        ```
        ```
        lscpu
        Architecture:          x86_64
        CPU op-mode(s):        32-bit, 64-bit
        Byte Order:            Little Endian
        CPU(s):                8
        On-line CPU(s) list:   0-7
        Thread(s) per core:    2
        Core(s) per socket:    4
        座：                 1
        NUMA 节点：         1
        厂商 ID：           GenuineIntel
        CPU 系列：          6
        型号：              85
        型号名称：        Intel(R) Xeon(R) Platinum 8163 CPU @ 2.50GHz
        步进：              4
        CPU MHz：             2499.996
        BogoMIPS：            4999.99
        超管理器厂商：  KVM
        虚拟化类型：     完全
        L1d 缓存：          32K
        L1i 缓存：          32K
        L2 缓存：           1024K
        L3 缓存：           33792K
        NUMA 节点0 CPU：    0-7
        Flags:                 fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc rep_good nopl eagerfpu pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm mpx avx512f avx512dq rdseed adx smap avx512cd avx512bw avx512vl xsaveopt xsavec xgetbv1
        ```
        >

2. Operation logs
    - [ ] please provide config file of syncer.
    ```
        log-level = "debug"
        server-id = 2279660052
        meta = "./syncer.meta"
        worker-count = 16
        batch = 10
        status-addr = "127.0.0.1:10086"
        skip-sqls = ["ALTER USER", "CREATE USER"]
        replicate-ignore-db = ["mysql","xedk_pre"]
        [[replicate-ignore-table]]
        db-name ="ttg_test"
        tbl-name = "t_loan_contract"
        [from]
        host = "10.36.1.20"
        user = "happigo"
        password = "***"
        port = 3306
        [to]
        host = "10.36.1.60"
        user = "root"
        password = "***"
        port = 3306
    ```
    - [ ] Please upload `syncer.log` if possible.
    ```
    2018/11/07 10:08:25 printer.go:52: [info] Welcome to syncer
    2018/11/07 10:08:25 printer.go:53: [info] Release Version: v1.0.0-32-g714b355
    2018/11/07 10:08:25 printer.go:54: [info] Git Commit Hash: 714b355bd014c5f198994fbdb219244f7cc50976
    2018/11/07 10:08:25 printer.go:55: [info] Git Branch: master
    2018/11/07 10:08:25 printer.go:56: [info] UTC Build Time: 2018-09-06 09:52:18
    2018/11/07 10:08:25 printer.go:57: [info] Go Version: go version go1.11 linux/amd64
    2018/11/07 10:08:25 main.go:55: [info] config: {"log-level":"debug","log-file":"syncer.log","log-rotate":"day","status-addr":"127.0.0.1:10086","server-id":2279660052,"meta":"./syncer.meta","persistent-dir":"","flavor":"mysql","worker-count":16,"batch":10,"max-retry":100,"replicate-do-table":null,"replicate-do-db":null,"replicate-ignore-table":null,"replicate-ignore-db":["mysql","xedk_pre"],"skip-sqls":["ALTER USER","CREATE USER"],"skip-dmls":null,"route-rules":null,"from":{"host":"10.36.1.20","user":"happigo","port":3306},"to":{"host":"10.36.1.60","user":"root","port":3306},"enable-gtid":false,"auto-fix-gtid":false,"disable-detect":false,"safe-mode":false,"config-file":"config.toml","stop-on-ddl":false,"execute-ddl-timeout":"3h","execute-dml-timeout":"1m"}
    2018/11/07 10:08:25 metrics.go:107: [info] listening on 127.0.0.1:10086 for status and metrics report.
    2018/11/07 10:08:25 syncer.go:910: [info] [syncer] last slave connection id 50486457
    2018/11/07 10:08:25 syncer.go:602: [info] rotate binlog to (mysql-bin.001628, 1321913)
   ...
    2018/11/07 10:08:25 syncer.go:606: [debug] source-db:mysql table:ha_health_check; target-db:mysql table:ha_health_check, RowsEvent data: [[1541552071915 m] [1541552093789 m]]
    2018/11/07 10:08:25 syncer.go:753: [debug] [XID event][pos](mysql-bin.001628, 1324400) [gtid set]ec179440-a357-11e7-8154-7cd30ac30aa0:1-4036968,1b29b1ff-df6c-11e7-8917-a0369fa51514:1-1220798,d1537353-a357-11e7-8153-70106faece8e:1-621893
    2018/11/07 10:08:25 ddl.go:103: [warning] will split alter table statement: ALTER TABLE `t_loan_contract` MODIFY COLUMN `BEGIN_DATE`  varchar(8) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT '开始日期' AFTER `RATE`
    2018/11/07 10:08:25 ast.go:509: [info] spec &{node:{text:} Tp:8 Name: Constraint:<nil> Options:[] NewTable:<nil> NewColumns:[0xc0008ac8c0] OldColumnName:<nil> Position:0xc0007b4e40 LockType:0 Comment: FromKey: ToKey: PartDefinitions:[]}
    2018/11/07 10:08:25 ast.go:76: [debug] tp 15, flag 0, flen 8, decimal -1, charset utf8, collate utf8_general_ci, strs [varchar(8)]
    2018/11/07 10:08:25 ast.go:515: [debug] alter table stmt to sql:[ALTER TABLE `t_loan_contract` MODIFY COLUMN `BEGIN_DATE` varchar(8) NOT NULL COMMENT '开始日期' AFTER `RATE`]
    2018/11/07 10:08:25 ddl.go:107: [warning] splitted alter table statement: [ALTER TABLE `t_loan_contract` MODIFY COLUMN `BEGIN_DATE` varchar(8) NOT NULL COMMENT '开始日期' AFTER `RATE`]
    2018/11/07 10:08:25 syncer.go:701: [info] [query]ALTER TABLE `t_loan_contract` MODIFY COLUMN `BEGIN_DATE`  varchar(8) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT '开始日期' AFTER `RATE` [current pos](mysql-bin.001628, 1324400) [next pos](mysql-bin.001628, 1324686) [current gtid set]d1537353-a357-11e7-8153-70106faece8e:1-621893,ec179440-a357-11e7-8154-7cd30ac30aa0:1-4036968,1b29b1ff-df6c-11e7-8917-a0369fa51514:1-1220798 [next gtid set]<nil>
    2018/11/07 10:08:25 syncer.go:737: [info] [ddl][schema]ttg_test [start]USE `ttg_test`; ALTER TABLE `t_loan_contract` MODIFY COLUMN `BEGIN_DATE` varchar(8) NOT NULL COMMENT '开始日期' AFTER `RATE`;
    2018/11/07 10:08:25 db.go:126: [debug] [exec][sql]USE `ttg_test`; ALTER TABLE `t_loan_contract` MODIFY COLUMN `BEGIN_DATE` varchar(8) NOT NULL COMMENT '开始日期' AFTER `RATE`;[args][]
    2018/11/07 10:08:25 db.go:130: [warning] [exec][sql]USE `ttg_test`; ALTER TABLE `t_loan_contract` MODIFY COLUMN `BEGIN_DATE` varchar(8) NOT NULL COMMENT '开始日期' AFTER `RATE`;[args][][error]Error 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'ALTER TABLE `t_loan_contract` MODIFY COLUMN `BEGIN_DATE` varchar(8) NOT NULL COM' at line 1
    2018/11/07 10:08:25 db.go:102: [error] [exec][sql][USE `ttg_test`; ALTER TABLE `t_loan_contract` MODIFY COLUMN `BEGIN_DATE` varchar(8) NOT NULL COMMENT '开始日期' AFTER `RATE`;][args][[]][error]Error 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'ALTER TABLE `t_loan_contract` MODIFY COLUMN `BEGIN_DATE` varchar(8) NOT NULL COM' at line 1
    2018/11/07 10:08:25 syncer.go:447: [fatal] Error 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'ALTER TABLE `t_loan_contract` MODIFY COLUMN `BEGIN_DATE` varchar(8) NOT NULL COM' at line 1
    /home/jenkins/workspace/build_tidb_enterprise_tools_master/go/src/github.com/pingcap/tidb-enterprise-tools/syncer/db.go:136: 
    /home/jenkins/workspace/build_tidb_enterprise_tools_master/go/src/github.com/pingcap/tidb-enterprise-tools/syncer/db.go:103: 
    ```
    - [ ] Please upload monitor screenshots. if not deployed, please add prometheus monitor and [grafana dashboard](https://github.com/pingcap/tidb-ansible/blob/master/scripts/syncer.json)
    - [ ] Other interesting logs

3. Common issues
    - [ ] Is the `worker-count` set to a reasonable value (suggest-32)? 
    ```
      work-count=16
    ```
    - [ ] Is the `batch` set to a reasonable value (suggest 100-1000)?
    ```
      batch=10
    ```
