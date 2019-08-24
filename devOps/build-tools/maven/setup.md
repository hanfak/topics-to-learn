 http://maven.apache.org/download.cgi  and download

 extract and download to `	/usr/local/apache-maven`

 Set env variables

For linux/mac
```
export M2_HOME=/usr/local/apache-maven-install-path
export M2=$M2_HOME/bin
export MAVEN_OPTS=-Xms256m -Xmx512m
```

Setup command line tools

```
export PATH=$M2:$PATH
```

verifying installation

```
mvn --version
```
