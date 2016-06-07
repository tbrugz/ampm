
mvnrun
======

**mvnrun** is a cli frontend to some package management tasks based on [maven](https://maven.apache.org/)
repositories. Specially, you may use it to install, uninstall, run, & create executable for java artifacts.


using mvnrun
------

- depends on: java, maven, [ant](https://ant.apache.org/)

- download [Maven Ant Tasks](http://maven.apache.org/ant-tasks/) into `$HOME/.ant/lib`
  ([direct link](http://central.maven.org/maven2/org/apache/maven/maven-ant-tasks/2.1.3/maven-ant-tasks-2.1.3.jar))  
  e.g.: `curl -o $HOME/.ant/lib/maven-ant-tasks-2.1.3.jar http://central.maven.org/maven2/org/apache/maven/maven-ant-tasks/2.1.3/maven-ant-tasks-2.1.3.jar`

- clone this repo to some dir (`<mvnrun-dir>`)  
  `git clone https://github.com/tbrugz/mvnrun.git <mvnrun-dir>`

- run it (from `<mvnrun-dir>` for now)


examples
------

#### jetty runner

Examples using [Jetty Runner](http://www.eclipse.org/jetty/documentation/9.3.9.v20160517/runner.html)

Test if jetty-runner is installed:  
`ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 is-installed`

Install jetty-runner and its dependencies:  
`ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 install`

Run jetty-runner:  
`ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 -Dmainclass=org.eclipse.jetty.runner.Runner -Dargs="--port 8081 <some-dir>" run`

Create executable script:  
`ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 -Dmainclass=org.eclipse.jetty.runner.Runner make-exec`

Run the executable script created:  
`org.eclipse.jetty.jetty-runner.9.3.10.M0.sh --port 8081 <some-dir>`  
or: `org.eclipse.jetty.jetty-runner.9.3.10.M0.bat --port 8081 <some-dir>` (windows)

Uninstall jetty-runner (not its dependencies):  
`ant -DgroupId=org.eclipse.jetty -DartifactId=jetty-runner -Dversion=9.3.10.M0 uninstall`

You mmay search for jetty runner artifacts in
[maven central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22org.eclipse.jetty%22%20AND%20a%3A%22jetty-runner%22)
or [mvnrepository.com](http://mvnrepository.com/artifact/org.eclipse.jetty/jetty-runner)

#### javadev/calc

Install calc:  
`ant -DgroupId=com.github.javadev -DartifactId=calc -Dversion=1.0 install`

Run calc:  
`ant -DgroupId=com.github.javadev -DartifactId=calc -Dversion=1.0 -Dmainclass=com.github.calc.Calc run`

#### Microemu

Install microemulator:  
`ant -DgroupId=org.microemu -DartifactId=microemulator-app-swing -Dversion=2.0.0 install`

Run microemulator:  
`ant -DgroupId=org.microemu -DartifactId=microemulator-app-swing -Dversion=2.0.0 -Dmainclass=org.microemu.app.Main run`


end notes
------

Author: Telmo Brugnara <tbrugz@gmail.com>
License: [Apache License, v2.0](http://www.apache.org/licenses/LICENSE-2.0)
