<!--
title: "Contrast Maven Plugin"
description: "Sample Maven build plugin using the Contrast Java SDK"
tags: "tools Maven SDK Integration Java"
-->

## About The Contrast Maven Plugin

The Contrast Maven Plugin is used to integrate the Contrast jar with your build. It is capable of authenticating a user to TeamServer, downloading the latest Java agent, and verifying your build.

[Maven](https://maven.apache.org/) is a build tool that utilizes `pom.xml` files to configure your applications. It is used to build, package, and test Java applications.

## Access To The Plugin

The plugin code can be viewed in our Github [repository](https://github.com/Contrast-Security-OSS/contrast-maven-plugin). Here you can review how our two goals, `install` and `verify` work.

<!-- The plugin can be found here on the Maven repository. -->

## How To Use The Plugin

### Configuration

Below is a table showing all the different parameters for the plugin. These settings are for connecting to TeamServer and filtering your vulnerabilities.

| Parameter                    | Description                                             |
|------------------------------|---------------------------------------------------------|
| TeamServer Username          | This is the username/email for your user in TeamServer |
| TeamServer Service Key       | Service Key found in Organization Settings             |
| TeamServer API Key           | API Key found in Organization Settings                 |
| TeamServer API Url           | API Url to your TeamServer instance                    |
| TeamServer Organization Uuid | Organization Uuid of the configured user found in Organization Settings |
| Application Name             | Name of application you set with ```-Dcontrast.appname``` <BR> This is used to filter for your application |
| Minimum Severity Level       | Minimum Severity level to filter for (NOTE, LOW, MEDIUM, HIGH, CRITICAL). This property is inclusive. |
| Server Name                  | Name of server you set with ```-Dcontrast.server``` <BR> Use *app.contrastsecurity.com/Contrast/api* if you are a SaaS customer |
| Jar Path                     | Path of a local jar file if you don't want to download the agent again                  |


>**Note**: Even if your build succeeds, the plugin will fail the overall build if a bad condition is found.


Below is a sample TeamServer configuration for the Contrast Maven Plugin:

```xml
<plugin>
    <groupId>com.contrastsecurity</groupId>
    <artifactId>contrast-maven-plugin</artifactId>
    <version>1.3</version>
    <executions>
        <execution>
            <id>install-contrast-jar</id>
            <goals>
                <goal>install</goal>
            </goals>
        </execution>
        <execution>
            <id>verify-with-contrast</id>
            <phase>post-integration-test</phase>
            <goals>
                <goal>verify</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <username>test_user</username>
        <apiKey>testApiKey</apiKey>
        <serviceKey>testServiceKEy</serviceKey>
        <apiUrl>http://www.app.contrastsecurity.com/Contrast/api</apiUrl>
        <orgUuid>QWER-ASDF-ZXCV-ERTY</orgUuid>
        <appName>Test Application</appName>
        <serverName>jenkins.slave1</serverName>
        <minSeverity>HIGH</minSeverity>
    </configuration>
</plugin>
```
