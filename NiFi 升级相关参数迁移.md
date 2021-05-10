# NiFi 升级相关参数迁移

## 选用工具

[Apache NiFi Toolkit Guide](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html)

```bash
# 进入工具命令行
./bin/cli.sh

# 查看帮助信息
help
```

### list-param-contexts

```bash
#> nifi list-param-contexts -h

Lists the parameter contexts that the current user is authorized to retrieve.

PRODUCES BACK-REFERENCES

usage: list-param-contexts
 -bap,--basicAuthPassword <arg>   The password for basic auth
 -bau,--basicAuthUsername <arg>   The username for basic auth
 -btk,--bearerToken <arg>         The bearer token to be passed in the
                                  Authorization header of a request
 -cto,--connectionTimeout <arg>   Timeout parameter for creating a connection to
                                  NiFi/Registry, specified in milliseconds
 -h,--help                        Help
 -kp,--keyPasswd <arg>            The key password of the keystore being used
 -ks,--keystore <arg>             A keystore to use for TLS/SSL connections
 -ksp,--keystorePasswd <arg>      The password of the keystore being used
 -kst,--keystoreType <arg>        The type of key store being used such as
                                  PKCS12
 -ot,--outputType <arg>           The type of output to produce (json or simple)
 -p,--properties <arg>            A properties file to load arguments from,
                                  command line values will override anything in
                                  the properties file, must contain full path to
                                  file
 -pe,--proxiedEntity <arg>        The identity of an entity to proxy
 -rto,--readTimeout <arg>         Timeout parameter for reading from
                                  NiFi/Registry, specified in milliseconds
 -ts,--truststore <arg>           A truststore to use for TLS/SSL connections
 -tsp,--truststorePasswd <arg>    The password of the truststore being used
 -tst,--truststoreType <arg>      The type of trust store being used such as
                                  PKCS12
 -u,--baseUrl <arg>               The URL to execute the command against
 -verbose,--verbose               Indicates that verbose output should be
                                  provided
```

### export-param-context

```bash
nifi export-param-context -h

Exports a given parameter context to a json representation, with the option of
writing to a file.

usage: export-param-context
 -bap,--basicAuthPassword <arg>   The password for basic auth
 -bau,--basicAuthUsername <arg>   The username for basic auth
 -btk,--bearerToken <arg>         The bearer token to be passed in the
                                  Authorization header of a request
 -cto,--connectionTimeout <arg>   Timeout parameter for creating a connection to
                                  NiFi/Registry, specified in milliseconds
 -h,--help                        Help
 -kp,--keyPasswd <arg>            The key password of the keystore being used
 -ks,--keystore <arg>             A keystore to use for TLS/SSL connections
 -ksp,--keystorePasswd <arg>      The password of the keystore being used
 -kst,--keystoreType <arg>        The type of key store being used such as
                                  PKCS12
 -o,--outputFile <arg>            A file to write output to, must contain full
                                  path and filename
 -ot,--outputType <arg>           The type of output to produce (json or simple)
 -p,--properties <arg>            A properties file to load arguments from,
                                  command line values will override anything in
                                  the properties file, must contain full path to
                                  file
 -pcid,--paramContextId <arg>     The id of a parameter context
 -pe,--proxiedEntity <arg>        The identity of an entity to proxy
 -rto,--readTimeout <arg>         Timeout parameter for reading from
                                  NiFi/Registry, specified in milliseconds
 -ts,--truststore <arg>           A truststore to use for TLS/SSL connections
 -tsp,--truststorePasswd <arg>    The password of the truststore being used
 -tst,--truststoreType <arg>      The type of trust store being used such as
                                  PKCS12
 -u,--baseUrl <arg>               The URL to execute the command against
 -verbose,--verbose               Indicates that verbose output should be
                                  provided
```

### import-param-context

```bash
#> nifi import-param-context -h

Imports a parameter context using the output from the export-param-context
command as the context to import. If the context name and context description
arguments are specified, they will override what is in the context json.

usage: import-param-context
 -bap,--basicAuthPassword <arg>         The password for basic auth
 -bau,--basicAuthUsername <arg>         The username for basic auth
 -btk,--bearerToken <arg>               The bearer token to be passed in the
                                        Authorization header of a request
 -cto,--connectionTimeout <arg>         Timeout parameter for creating a
                                        connection to NiFi/Registry, specified
                                        in milliseconds
 -h,--help                              Help
 -i,--input <arg>                       A local file to read as input contents,
                                        or a public URL to fetch
 -kp,--keyPasswd <arg>                  The key password of the keystore being
                                        used
 -ks,--keystore <arg>                   A keystore to use for TLS/SSL
                                        connections
 -ksp,--keystorePasswd <arg>            The password of the keystore being used
 -kst,--keystoreType <arg>              The type of key store being used such as
                                        PKCS12
 -ot,--outputType <arg>                 The type of output to produce (json or
                                        simple)
 -p,--properties <arg>                  A properties file to load arguments
                                        from, command line values will override
                                        anything in the properties file, must
                                        contain full path to file
 -pcd,--paramContextDescription <arg>   The description of a parameter context
 -pcn,--paramContextName <arg>          The name of a parameter context
 -pe,--proxiedEntity <arg>              The identity of an entity to proxy
 -rto,--readTimeout <arg>               Timeout parameter for reading from
                                        NiFi/Registry, specified in milliseconds
 -ts,--truststore <arg>                 A truststore to use for TLS/SSL
                                        connections
 -tsp,--truststorePasswd <arg>          The password of the truststore being
                                        used
 -tst,--truststoreType <arg>            The type of trust store being used such
                                        as PKCS12
 -u,--baseUrl <arg>                     The URL to execute the command against
 -verbose,--verbose                     Indicates that verbose output should be
                                        provided

```









## 查看当前参数列表

```bash
./bin/cli.sh nifi list-param-contexts -u http://localhost:8080 -ot simple

# ========= 输出信息 =======
#   Id                                     Name                Description
-   ------------------------------------   -----------------   -----------
1   d5685e6b-6cd3-39a8-1e96-a84abba4b05b   ddi global params
2   058aeabd-a0ea-3709-a03f-6bbebe5a6297   tech_util_params
```



## 查看指定context参数

```bash
./bin/cli.sh nifi export-param-context -u http://localhost:8080 -verbose --paramContextId d5685e6b-6cd3-39a8-1e96-a84abba4b05b
```

```json
{
  "name" : "ddi global params",
  "description" : "",
  "parameters" : [ {
    "parameter" : {
      "name" : "Max_Connections",
      "description" : "",
      "sensitive" : false,
      "value" : "1"
    }
  }, {
    "parameter" : {
      "name" : "driver.jar",
      "description" : "",
      "sensitive" : false,
      "value" : "/opt/nifi-1.11.4/mylib/mysql-connector-java-8.0.15.jar"
    }
  }, {
    "parameter" : {
      "name" : "heartbeat.db.password",
      "description" : "",
      "sensitive" : true
    }
  }, {
    "parameter" : {
      "name" : "heartbeat.db.user",
      "description" : "",
      "sensitive" : false,
      "value" : "etl"
    }
  }, {
    "parameter" : {
      "name" : "olap_batch_reload_by_user_Listening_Port",
      "description" : "",
      "sensitive" : false,
      "value" : "60003"
    }
  }, {
    "parameter" : {
      "name" : "source.db.backup.jdbc.url",
      "description" : "",
      "sensitive" : false,
      "value" : "jdbc:mysql://10.0.1.10:8306/ddiprod?useUnicode=true&characterEncoding=utf8&serverTimezone=Asia/Shanghai"
    }
  }, {
    "parameter" : {
      "name" : "source.db.jdbc.url",
      "description" : "",
      "sensitive" : false,
      "value" : "jdbc:mysql://10.0.1.5:3306/ddiprod?useUnicode=true&characterEncoding=utf8&serverTimezone=Asia/Shanghai"
    }
  }, {
    "parameter" : {
      "name" : "source.db.password",
      "description" : "",
      "sensitive" : true
    }
  }, {
    "parameter" : {
      "name" : "source.db.trail.jdbc.url",
      "description" : "",
      "sensitive" : false,
      "value" : "jdbc:mysql://52.130.87.138:3306/ddiprod?useUnicode=true&characterEncoding=utf8&serverTimezone=Asia/Shanghai"
    }
  }, {
    "parameter" : {
      "name" : "source.db.user",
      "description" : "",
      "sensitive" : false,
      "value" : "root"
    }
  }, {
    "parameter" : {
      "name" : "source.heartbeat.db.jdbc.url",
      "description" : "",
      "sensitive" : false,
      "value" : "jdbc:mysql://rm-uf64804rnp5g9l127vo.mysql.rds.aliyuncs.com:3306/heartbeat_prod?useUnicode=true&characterEncoding=utf8"
    }
  }, {
    "parameter" : {
      "name" : "sourceMinimumIdleConnections",
      "description" : "",
      "sensitive" : false,
      "value" : "1"
    }
  }, {
    "parameter" : {
      "name" : "source_db_catalog",
      "description" : "",
      "sensitive" : false,
      "value" : "ddiprod"
    }
  } ]
}
```

## 实用使用命令

```bash
#   Id                                     Name                Description
-   ------------------------------------   -----------------   -----------
1   d5685e6b-6cd3-39a8-1e96-a84abba4b05b   ddi global params
2   058aeabd-a0ea-3709-a03f-6bbebe5a6297   tech_util_params

# 导出localhost环境参数
./bin/cli.sh nifi export-param-context -u http://10.0.1.23:8080  --paramContextId d5685e6b-6cd3-39a8-1e96-a84abba4b05b -ot json -o ddi_global_params.json

# 导入环境参数到10.0.1.23服务器
./bin/cli.sh nifi import-param-context -u http://localhost:8080 -i ddi_global_params.json
```



```bash
cli.sh nifi list-param-contexts -u http://10.0.1.23:8080 -ot simple

#   Id                                     Name                Description
-   ------------------------------------   -----------------   -----------
1   d5685e6b-6cd3-39a8-1e96-a84abba4b05b   ddi global params
2   058aeabd-a0ea-3709-a03f-6bbebe5a6297   tech_util_params

cli.sh nifi export-param-context -u http://10.0.1.23:8080  --paramContextId d5685e6b-6cd3-39a8-1e96-a84abba4b05b -ot json -o ddi_global_params.json
cli.sh nifi export-param-context -u http://10.0.1.23:8080  --paramContextId 058aeabd-a0ea-3709-a03f-6bbebe5a6297  -ot json -o tech_util_params.json


```



## Reference

[DevOps: Working with Parameter Contexts in Apache NiFi 1.11.4+](https://www.datainmotion.dev/2020/09/devops-working-with-parameter-contexts.html)

