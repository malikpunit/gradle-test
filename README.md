### 

* 2 functions  - doFirst, doLast - these run different parts of lifecycle
* plugins  - introduce tasks to gradle
* can optionally have settings.file
* build file(build.gradle) define tasks used for project either defined directly OR through plugins
### 3 build phases initialization -> configuration -> execution
  * intialization phase
    - evaluates which projects will be part of this build 
    - single project - makes project part of build 
    - multiple project build - determines which projects within multi project build will part of execution
  * configuration phase 
    - projects are configured
    - done by execution buildscripts of all the projects that are part of this build
  * execution phase
    - gradle works out which tasks are to be executed
    - based on task name passed as an argument on gradle command line
    - a given task has multiple phases of execution
      1. doFirst - use this closure for things to be run at the start of the task execution
      2. doLast - use this closure for things to be run at the end of the task execution
      3. condition based - things to be run on certain conditions
    - dependsOn ensures a task run after another, but in between other tasks may run

### List  Tasks
`gradle tasks`

### Build Gradle project 
`gradle build`
`gradle build -i`
`gradle clean build`

### Plugin

- java, application are plugins known to gradle, others have to be specied with full name and version
- If application plugin is defined, run task can be used to run java process provided mainClassName is set.

### Dependencies
* can be satisfied from multiple places
  * Other projects
  * File system
  * Maven repositories
  * Ivy repositories
* project can depend on other projects, external libraries OR internal libraries

* dependencies can have many configuration
  * compilation
  * runtime
  * Test compilation
  * Test runtime
* can be cached
*Transitive Dependencies* - some dependencies depend on others and downloads them as well.
* dependencies can be known by `gradle -q dependencies`
*  dependencies can only be known for specific configuration by `gradle -q dependencies --configuration complieClasspath`
* dependencies are resolved from 
  * Remote
  * Local(local maven cache on file system)
  * File system(flatDir)
* dependency lies in configurations scopes
  * implementation - if defined at this scope used at both compile time and runtime
    - compileOnly - if defined at this scope used at only compile time
    - runtimeOnly - if defined at this scope used at only runtime
  * testImplementation
    - testCompileOnly - if defined at this scope used at only test compile time
    - testRuntimeOnly - if defined at this scope used at only test runtime
  
