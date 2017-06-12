
Install
-------

Clone repo

```
git clone https://github.com/tbrugz/mvnrun.git mvnrun
```

Install AMPM on `$HOME/bin`

```
cd mvnrun
mkdir -p $HOME/bin
export AMPM_DIR=$(pwd)
cp $AMPM_DIR/ampm $HOME/bin
cp $AMPM_DIR/build.xml $HOME/bin
```

Usage
-----

**ampm [general-options] <action/target> [target options/arguments]**

general-options:

* VM system properties (starting with `-D`)
  * `-Dmainclass=<mainclass>` - set class with `main()` method - useful with *run* & *make-exec*
  * `-Dclasspath=<extra classpath>` - set extra classpath for *run* & *make-exec*

actions/targets:

* **check-latest-version**  Checks artifact's latest version in Maven Central
* **info**                  Shows basic environment info
* **install**               Installs (downloads into local repo) the artifact
* **is-installed**          Tests if artifact is installed
* **list**                  List artifacts in the local repo
* **list-organizations**    List organizations with artifacts in the local repo
* **make-exec**             Creates an executable script from an artifact
* **run**                   Executes the mainclass of an application/artifact
* **show**                  Show artifact info
* **uninstall**             Uninstalls an artifact (not its dependencies)

target options/arguments (by option types):

 `info`

 `list-organizations    <org*> [<artf*>]`  
 `list                  <org*> [<artf*>]`

 `check-latest-version  <org> <artf>`

 `install               <org> <artf> [ <vers> | latest ]`  
 `is-installed          <org> <artf> [ <vers> | latest ]`  
 `show                  <org> <artf> [ <vers> | latest ]`  
 `uninstall             <org> <artf> [ <vers> | latest ]`

 `make-exec             <org> <artf> [ <vers> | latest ]`

 `run                   <org> <artf> [ <vers> | latest ] <arguments>`


Examples
--------
(Assumes `ampm` is in the `$PATH`)

#### jetty runner

Examples using [Jetty Runner](http://www.eclipse.org/jetty/documentation/9.3.9.v20160517/runner.html)

Test if jetty-runner is installed:  
`ampm is-installed org.eclipse.jetty jetty-runner 9.3.10.M0`  
or: `ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 is-installed`

Check latest version avaiable in central:
`ampm check-latest-version org.eclipse.jetty jetty-runner`  
or: `ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner check-latest-version`  
or: `ant -Dartifact=org.eclipse.jetty:jetty-runner check-latest-version`

Install jetty-runner and its dependencies:  
`ampm install org.eclipse.jetty jetty-runner 9.3.10.M0`  
or: `ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 install`  
or: `ant -Dartifact=org.eclipse.jetty:jetty-runner:9.3.10.M0 install`

Run jetty-runner (replace `<some-dir>`):  
`ampm -Dmainclass=org.eclipse.jetty.runner.Runner run org.eclipse.jetty jetty-runner 9.3.10.M0 --port 8081 <some-dir>`  
or: `ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 -Dmainclass=org.eclipse.jetty.runner.Runner -Dargs="--port 8081 <some-dir>" run`  
(and navigate to `http://localhost:8081/`)

Run jetty-runner without `mainclass` property - extracted from MANIFEST (replace `<some-dir>`):  
`ampm run org.eclipse.jetty jetty-runner 9.3.10.M0 --port 8081 <some-dir>`  
or: `ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 -Dargs="--port 8081 <some-dir>" run`  
or: `ant -Dartifact=org.eclipse.jetty:jetty-runner:9.3.10.M0 -Dargs="--port 8081 ." run`  
(and navigate to `http://localhost:8081/`)

Create executable script:  
`ampm -Dmainclass=org.eclipse.jetty.runner.Runner make-exec org.eclipse.jetty jetty-runner 9.3.10.M0`  
or: `ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 -Dmainclass=org.eclipse.jetty.runner.Runner make-exec`  
or: `ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 make-exec`

Run the executable script created (replace `<some-dir>` - assumes `$HOME/bin` is in the `$PATH`):  
`org.eclipse.jetty.jetty-runner.9.3.10.M0.sh --port 8081 <some-dir>`  
or (windows): `org.eclipse.jetty.jetty-runner.9.3.10.M0.bat --port 8081 <some-dir>`

Uninstall jetty-runner (not its dependencies):  
`ampm uninstall org.eclipse.jetty jetty-runner 9.3.10.M0`
or: `ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 uninstall`

You may search for jetty runner artifacts in
[maven central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22org.eclipse.jetty%22%20AND%20a%3A%22jetty-runner%22)
or [mvnrepository.com](http://mvnrepository.com/artifact/org.eclipse.jetty/jetty-runner)

#### javadev/calc

Examples using swing app [javadev/calc](https://github.com/javadev/calc)

Install calc:  
`ampm install com.github.javadev calc 1.0`  
or: `ant -DgroupId=com.github.javadev -DartifactId=calc -Dversion=1.0 install`

Run calc:  
`ampm -Dmainclass=com.github.calc.Calc run com.github.javadev calc 1.0`  
or: `ampm run com.github.javadev calc 1.0`  
or: `ant -DgroupId=com.github.javadev -DartifactId=calc -Dversion=1.0 -Dmainclass=com.github.calc.Calc run`  
or: `ant -DgroupId=com.github.javadev -DartifactId=calc -Dversion=1.0 run`

#### sqlline

Examples using [sqlline](https://github.com/julianhyde/sqlline)

Install sqlline:  
`ampm install sqlline sqlline 1.1.9`  
or: `ant -DgroupId=sqlline -DartifactId=sqlline -Dversion=1.1.9 install`

Run sqlline (using extra `classpath` - replace `<dir-with-drivers-jars>`):  
`ampm -Dmainclass=sqlline.SqlLine -Dclasspath=<dir-with-drivers-jars>/* run sqlline sqlline 1.1.9`  
or: `ant -DgroupId=sqlline -DartifactId=sqlline -Dversion=1.1.9 -Dmainclass=sqlline.SqlLine -Dclasspath=<dir-with-drivers-jars>/* run`

Create executable script (replace `<dir-with-drivers-jars>`):  
`ampm -Dmainclass=sqlline.SqlLine -Dclasspath=<dir-with-drivers-jars>/* make-exec sqlline sqlline 1.1.9`
or: `ant -DgroupId=sqlline -DartifactId=sqlline -Dversion=1.1.9 -Dmainclass=sqlline.SqlLine -Dclasspath=<dir-with-drivers-jars>/* make-exec`

Create executable script with name `sqlline.[sh|bat]` (replace `<dir-with-drivers-jars>`):  
`ampm -Dmainclass=sqlline.SqlLine -Dclasspath=<dir-with-drivers-jars>/* -Dbase.script.file=sqlline make-exec sqlline sqlline 1.1.9`
or: `ant -DgroupId=sqlline -DartifactId=sqlline -Dversion=1.1.9 -Dmainclass=sqlline.SqlLine -Dclasspath=<dir-with-drivers-jars>/* -Dbase.script.file=sqlline make-exec`

#### h2

Examples using [h2](http://www.h2database.com/)

Install version `1.4.192` of h2:  
`ampm install com.h2database h2 1.4.192`  
or: `ant -DgroupId=com.h2database -DartifactId=h2 -Dversion=1.4.192 install`

Install latest version of h2 & Make executable:  
`ampm make-exec com.h2database h2 latest`  
or: `ant -DgroupId=com.h2database -DartifactId=h2 -DuseLatestVersion=1 make-exec`

Run h2 (see [options](http://www.h2database.com/javadoc/org/h2/tools/Server.html#main_String...)):  
`ampm run com.h2database h2 1.4.192 -tcpPort 9095`  
or: `ant -DgroupId=com.h2database -DartifactId=h2 -Dversion=1.4.192 -Dargs="-tcpPort 9095" run`  
or (if `make-exec` already executed): `com.h2database.h2.1.4.192.sh -tcpPort 9095`

Run h2 shell (make-exec & run using `exec.variant`):  
`ampm -Dmainclass=org.h2.tools.Shell -Dexec.variant=Shell make-exec com.h2database h2 1.4.192`  
or: `ant -DgroupId=com.h2database -DartifactId=h2 -Dversion=1.4.192 -Dmainclass=org.h2.tools.Shell -Dexec.variant=Shell make-exec`  
and: `com.h2database.h2.1.4.192.Shell.sh`

#### Microemu

Examples using [microemulator/microemu-javase-swing](https://github.com/tisoft/microemu/tree/master/microemulator/microemu-javase-swing)

Install microemulator:  
`ampm install org.microemu microemu-javase-swing 2.0.4`  
or: `ant -DgroupId=org.microemu -DartifactId=microemu-javase-swing -Dversion=2.0.4 install`

Run microemulator:  
`ampm -Dmainclass=org.microemu.app.Main run org.microemu microemu-javase-swing 2.0.4`  
or: `ant -DgroupId=org.microemu -DartifactId=microemu-javase-swing -Dversion=2.0.4 -Dmainclass=org.microemu.app.Main run`


Examples querying local repo (`~/.m2/repository` by default)
------

List organizations:  
`ampm list-organizations ch.qos.logback` (list/show `ch.qos.logback` organization)  
or: `ampm list-organizations org` (organizations from `org.`)  
or: `ampm list-organizations o*` (organizations starting with `o`)  
or: `ampm list-organizations` (list all)

List artifacts:  
`ampm list ch.qos.log*` (artifacts from organizations starting with `ch.qos.log`)  
or: `ampm -Dlist.maxVersionsToShow=7 list org.slf4j` (artifacts from `org.slf4j` - show up to 7 versions)  
or: `ampm list` (list all artifacts)

Show artifact details:  
`ampm show org.apache.cxf cxf 2.4.6`  
or: `ampm show org.apache.struts struts-core latest`

Info (default environment variables):  
`ampm info`  
or: `ant info`
