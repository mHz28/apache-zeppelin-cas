# Apache Zeppelin Shiro install

Configure and install Shiro in Zeppelin

## Installation

* git clone https://github.com/apache/zeppelin.git
* change dir to $INSTALL_DIR/conf
* mv shiro.ini.template shiro.ini
* edit shiro.ini add config below:
````
[main]
sessionManager = org.apache.shiro.web.session.mgt.DefaultWebSessionManager
securityManager.sessionManager = $sessionManager
securityManager.sessionManager.globalSessionTimeout = 86400000

[urls]
/api/shiro-cas

````
* cd $INSTALL_DIR/zeppelin-web
* edit pom.xml
* add the following config:
````
  <dependencies>
  <dependency>
    <groupId>org.apache.shiro</groupId>
    <artifactId>shiro-cas</artifactId>
    <version>1.2.3</version>
  </dependency>
</dependencies>
````

* cd to $INSTALL_DIR/zeppelin-web/
* mvn clean package -DskipTests
* cd to $INSTALL_DIR/zeppelin-web-angular/
* edit pom.xml
* add the following config:
````
  <dependencies>
  <dependency>
    <groupId>org.apache.shiro</groupId>
    <artifactId>shiro-cas</artifactId>
    <version>1.2.3</version>
  </dependency>
</dependencies>
````

* add authc endpoint in shiro.ini
````
#/** = anon
/** = authc

````

* apply multiple users in Shiro:
````
[main]
anyofrolesuser = org.apache.zeppelin.utils.AnyOfRolesUserAuthorizationFilter

[urls]

/apilogin = authc, anyofrolesuser[admin, user1]

````

* mvn clean package -DskipTests

## Start Service

* $INSTALL_DIR/bin/zeppelin-daemon.sh start

# Apache Zeppelin

**Documentation:** [User Guide](https://zeppelin.apache.org/docs/latest/index.html)<br/>
**Mailing Lists:** [User and Dev mailing list](https://zeppelin.apache.org/community.html)<br/>
**Continuous Integration:** ![core](https://github.com/apache/zeppelin/workflows/core/badge.svg) ![frontend](https://github.com/apache/zeppelin/workflows/frontend/badge.svg) ![rat](https://github.com/apache/zeppelin/workflows/rat/badge.svg) <br/>
**Contributing:** [Contribution Guide](https://zeppelin.apache.org/contribution/contributions.html)<br/>
**Issue Tracker:** [Jira](https://issues.apache.org/jira/browse/ZEPPELIN)<br/>
**License:** [Apache 2.0](https://github.com/apache/zeppelin/blob/master/LICENSE)


**Zeppelin**, a web-based notebook that enables interactive data analytics. You can make beautiful data-driven, interactive and collaborative documents with SQL, Scala and more.

Core features:
   * Web based notebook style editor.
   * Built-in Apache Spark support


To know more about Zeppelin, visit our web site [https://zeppelin.apache.org](https://zeppelin.apache.org)


## Getting Started

### Install binary package
Please go to [install](https://zeppelin.apache.org/docs/latest/quickstart/install.html) to install Apache Zeppelin from binary package.

### Build from source
Please check [Build from source](https://zeppelin.apache.org/docs/latest/setup/basics/how_to_build.html) to build Zeppelin from source.
