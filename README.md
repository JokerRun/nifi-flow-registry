## 1.clone flow 仓库



## 2.更名成flow_storage



## 3.调整conf/providers.xml

### 3.1.flowPersistenceProvider调整为GitFlowPersistenceProvider

```xml
    <flowPersistenceProvider>
        <class>org.apache.nifi.registry.provider.flow.git.GitFlowPersistenceProvider</class>
        <property name="Flow Storage Directory">./flow_storage</property>
        <property name="Remote To Push">origin</property>
        <property name="Remote Access User">******</property>
        <property name="Remote Access Password">******</property>
    </flowPersistenceProvider>
```

