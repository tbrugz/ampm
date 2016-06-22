
CHANGELOG
=========

### v-next

- [x] use http://repo1.maven.org/maven2/<org>/<artif>/maven-metadata.xml
    - latest, versions, lastUpdated
- [x] check M2_HOME for settings.xml
- [x] use "artifact" parameter


### v0.3

- [x] list organizations with artifacts in local repo
- [x] list installed artifacts of organization
    - [x] list installed versions of artifacts
    - [x] order versions in version-like order! not simply alphanumeric
- [x] show-artifact: pom info, latest-version on central...


### v0.2.5

- [x] generate ant tasks dependency graph - graphml
- [x] parse JSON with js - http://stackoverflow.com/questions/2527020/parse-json-with-ant


### v0.2

- [x] query search.maven.org for latest version of artifact
- [x] install (, run & make-exec) latest version of artifact
- [x] extract mainclass from jar/manifest
- [x] add -Dclasspath
- [x] task to install "maven-ant-tasks"
- [x] test if maven-ant-tasks is present
- [x] make-exec: add -Dexec.variant
- [x] rename xxx.yyy targets to xxx-yyy
- [x] check .m2/settings.xml for local repo location
