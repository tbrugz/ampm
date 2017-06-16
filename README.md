
ampm
======

**ampm** is a cli frontend to some package management tasks based on [maven](https://maven.apache.org/)
repositories. Specially, you may use it to install, uninstall, check latest version,
run & create executables for java artifacts.


using ampm
------

- depends on: java, maven, [ant](https://ant.apache.org/) (>=1.9.1)

- clone this repo to some dir (`<ampm-dir>`)  
  `git clone https://github.com/tbrugz/ampm.git <ampm-dir>`  
  or just download [build.xml](https://raw.githubusercontent.com/tbrugz/ampm/master/build.xml) to `<ampm-dir>`

- download [Maven Ant Tasks](http://maven.apache.org/ant-tasks/) into `$HOME/.ant/lib`
  ([direct link](http://central.maven.org/maven2/org/apache/maven/maven-ant-tasks/2.1.3/maven-ant-tasks-2.1.3.jar))  
  e.g.: `curl -o $HOME/.ant/lib/maven-ant-tasks-2.1.3.jar http://central.maven.org/maven2/org/apache/maven/maven-ant-tasks/2.1.3/maven-ant-tasks-2.1.3.jar`  
  or run (from `<ampm-dir>`): `ant install-maven-ant-tasks`

- run it (from `<ampm-dir>` for now)


examples
------

#### jetty runner

Examples using [Jetty Runner](http://www.eclipse.org/jetty/documentation/9.3.9.v20160517/runner.html)

Test if jetty-runner is installed:  
`ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 is-installed`

Check latest version avaiable in central:  
`ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner check-latest-version`  
or: `ant -Dartifact=org.eclipse.jetty:jetty-runner check-latest-version`

Install jetty-runner and its dependencies:  
`ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 install`  
or: `ant -Dartifact=org.eclipse.jetty:jetty-runner:9.3.10.M0 install`

Run jetty-runner (replace `<some-dir>`):  
`ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 -Dmainclass=org.eclipse.jetty.runner.Runner -Dargs="--port 8081 <some-dir>" run`  
(and navigate to `http://localhost:8081/`)

Run jetty-runner without `mainclass` property - extracted from MANIFEST (replace `<some-dir>`):  
`ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 -Dargs="--port 8081 <some-dir>" run`  
or: `ant -Dartifact=org.eclipse.jetty:jetty-runner:9.3.10.M0 -Dargs="--port 8081 ." run`  
(and navigate to `http://localhost:8081/`)

Create executable script:  
`ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 -Dmainclass=org.eclipse.jetty.runner.Runner make-exec`  
or: `ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 make-exec`

Run the executable script created (replace `<some-dir>`):  
`org.eclipse.jetty.jetty-runner.9.3.10.M0.sh --port 8081 <some-dir>`  
or (windows): `org.eclipse.jetty.jetty-runner.9.3.10.M0.bat --port 8081 <some-dir>`

Uninstall jetty-runner (not its dependencies):  
`ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 uninstall`

You may search for jetty runner artifacts in
[maven central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22org.eclipse.jetty%22%20AND%20a%3A%22jetty-runner%22)
or [mvnrepository.com](http://mvnrepository.com/artifact/org.eclipse.jetty/jetty-runner)

#### javadev/calc

Examples using swing app [javadev/calc](https://github.com/javadev/calc)

Install calc:  
`ant -DgroupId=com.github.javadev -DartifactId=calc -Dversion=1.0 install`

Run calc:  
`ant -DgroupId=com.github.javadev -DartifactId=calc -Dversion=1.0 -Dmainclass=com.github.calc.Calc run`  
or: `ant -DgroupId=com.github.javadev -DartifactId=calc -Dversion=1.0 run`

#### sqlline

Examples using [sqlline](https://github.com/julianhyde/sqlline)

Install sqlline:  
`ant -DgroupId=sqlline -DartifactId=sqlline -Dversion=1.1.9 install`

Run sqlline (using extra `classpath` - replace `<dir-with-drivers-jars>`):  
`ant -DgroupId=sqlline -DartifactId=sqlline -Dversion=1.1.9 -Dmainclass=sqlline.SqlLine -Dclasspath=<dir-with-drivers-jars>/* run`

Create executable script (replace `<dir-with-drivers-jars>`):  
`ant -DgroupId=sqlline -DartifactId=sqlline -Dversion=1.1.9 -Dmainclass=sqlline.SqlLine -Dclasspath=<dir-with-drivers-jars>/* make-exec`

Create executable script with name `sqlline.[sh|bat]` (replace `<dir-with-drivers-jars>`):  
`ant -DgroupId=sqlline -DartifactId=sqlline -Dversion=1.1.9 -Dmainclass=sqlline.SqlLine -Dclasspath=<dir-with-drivers-jars>/* -Dbase.script.file=sqlline make-exec`

#### h2

Examples using [h2](http://www.h2database.com/)

Install version `1.4.192` of h2:  
`ant -DgroupId=com.h2database -DartifactId=h2 -Dversion=1.4.192 install`

Install latest version of h2 & Make executable:  
`ant -DgroupId=com.h2database -DartifactId=h2 -DuseLatestVersion=1 install make-exec`

Run h2 (see [options](http://www.h2database.com/javadoc/org/h2/tools/Server.html#main_String...)):  
`ant -DgroupId=com.h2database -DartifactId=h2 -Dversion=1.4.192 -Dargs="-tcpPort 9095" run`  
or: `com.h2database.h2.1.4.192.sh -tcpPort 9095`

Run h2 shell (make-exec & run using `exec.variant`):  
`ant -DgroupId=com.h2database -DartifactId=h2 -Dversion=1.4.192 -Dmainclass=org.h2.tools.Shell -Dexec.variant=Shell make-exec`  
and: `com.h2database.h2.1.4.192.Shell.sh`

#### Microemu

Examples using [microemulator/microemu-javase-swing](https://github.com/tisoft/microemu/tree/master/microemulator/microemu-javase-swing)

Install microemulator:  
`ant -DgroupId=org.microemu -DartifactId=microemu-javase-swing -Dversion=2.0.4 install`

Run microemulator:  
`ant -DgroupId=org.microemu -DartifactId=microemu-javase-swing -Dversion=2.0.4 -Dmainclass=org.microemu.app.Main run`


examples querying local repo
------

List organizations:  
`ant -DgroupId=ch.qos.logback list-organizations` (list/show `ch.qos.logback` organization)  
or: `ant -DgroupId=org list-organizations` (organizations from `org.`)  
or: `ant -DgroupId=o* list-organizations` (organizations starting with `o`)  
or: `ant list-organizations` (list all)

List artifacts:  
`ant -DgroupId=ch.qos.log* list` (artifacts from organizations starting with `ch.qos.log`)  
or: `ant -DgroupId=org.slf4j -Dlist.maxVersionsToShow=7 list` (artifacts from `org.slf4j` - show up to 7 versions)  
or: `ant list` (list all artifacts)

Show artifact details:  
`ant -DgroupId=org.apache.cxf -DartifactId=cxf -Dversion=2.4.6 show`  
or: `ant -Dartifact=org.apache.cxf:cxf:2.4.6 show`  
or: `ant show -Dartifact=org.apache.struts:struts-core -DuseLatestVersion=1`


end notes
------

Author: Telmo Brugnara - <tbrugz@gmail.com>  
License: [Apache License, v2.0](http://www.apache.org/licenses/LICENSE-2.0)
