# 安装

## 依赖配置

?> 查询最高版本或历史版本方式：[Maven中央库](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.baomidou%22%20AND%20a%3A%22mybatis-plus%22) | [Maven阿里库](http://maven.aliyun.com/nexus/#nexus-search;quick~mybatis-plus)

```xml
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus</artifactId>
    <version>2.0.2</version>
</dependency>
```

!> 特别说明：**`Mybatis`及`Mybatis-Spring`依赖请勿加入项目配置，以免引起版本冲突！！！Mybatis-Plus会自动帮你维护！**

## 如何集成

Mybatis-Plus 的集成非常简单，对于 Spring，我们仅仅需要把 Mybatis 自带的`MybatisSqlSessionFactoryBean`替换为 MP 自带的即可。

!> MP 大部分配置都和传统 Mybatis 一致，少量配置为 MP 特色功能配置，**此处仅对 MP 的特色功能进行讲解，其余请参考 _Mybatis-Spring_ 配置说明**。

示例工程：

👉 [mybatisplus-spring-mvc](https://git.oschina.net/baomidou/mybatisplus-spring-mvc)

👉 [mybatisplus-spring-boot](https://git.oschina.net/baomidou/mybatisplus-spring-boot)

示例代码：

> Xml Config

```xml
<bean id="sqlSessionFactory" class="com.baomidou.mybatisplus.spring.MybatisSqlSessionFactoryBean">
    <!-- 配置数据源 -->
    <property name="dataSource" ref="dataSource"/>
    <!-- 自动扫描 Xml 文件位置 -->
    <property name="mapperLocations" value="classpath:mybatis/*/*.xml"/>
    <!-- 配置 Mybatis 配置文件（可无） -->
    <property name="configLocation" value="classpath:mybatis/mybatis-config.xml"/>
    <!-- 配置包别名 -->
    <property name="typeAliasesPackage" value="com.baomidou.springmvc.model"/>

    <!-- 以上配置和传统 Mybatis 一致 -->

    <!-- 插件配置 -->
    <property name="plugins">
        <array>
            <!-- 分页插件配置 -->
            <bean id="paginationInterceptor" class="com.baomidou.mybatisplus.plugins.PaginationInterceptor">
                <!-- 指定数据库方言 -->
                <property name="dialectType" value="mysql"/>
            </bean>
            <!-- 如需要开启其他插件，可配置于此 -->
        </array>
    </property>

    <!-- MP 全局配置注入 -->
    <property name="globalConfig" ref="globalConfig" />
</bean>

<!-- 定义 MP 全局策略 -->
<bean id="globalConfig" class="com.baomidou.mybatisplus.entity.GlobalConfiguration">
    <!-- 主键策略配置 -->
    <!-- 可选参数
        AUTO->`0`("数据库ID自增")
        INPUT->`1`(用户输入ID")
        ID_WORKER->`2`("全局唯一ID")
        UUID->`3`("全局唯一ID")
    -->
    <property name="idType" value="2" />

    <!-- 数据库类型配置 -->
    <!-- 可选参数（默认mysql）
        MYSQL->`mysql`
        ORACLE->`oracle`
        DB2->`db2`
        H2->`h2`
        HSQL->`hsql`
        SQLITE->`sqlite`
        POSTGRE->`postgresql`
        SQLSERVER2005->`sqlserver2005`
        SQLSERVER->`sqlserver`
    -->
    <property name="dbType" value="oracle" />

    <!-- 全局表为下划线命名设置 true -->
    <property name="dbColumnUnderline" value="true" />
</bean>
```

!> 特别注意 `MybatisSqlSessionFactoryBean` 非原生的类，必须如上配置 ！

> Java Config

```java
// TODO
```
