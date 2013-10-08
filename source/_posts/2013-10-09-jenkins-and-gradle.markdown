---
layout: post
title: "jenkins and gradle"
date: 2013-10-09 01:08
comments: true
categories: 
---

Install jenkins

<pre>
sudo zypper addrepo http://pkg.jenkins-ci.org/opensuse/ jenkins
sudo zypper install jenkins
</pre>

"Manage Jenkins", "Manage Plugins"

"Advanced", "Update Site", Url is http://mirror.xmission.com/jenkins/updates/update-center.json, Install "Gradle Plugin",  "Git Plugin", "Post build task", Install gradle 1.8 /var/lib/jenkins/tools/hudson.plugins.gradle.GradleInstallation/gradle-1.8
  
"New job"

"Source Code Management", "git repo" is git@host:test.git, "Branches to build" is origin/develop. "Build", "Invoke Gradle script", "Task" is build and deploy 

<pre>
// /var/lib/jenkins/jobs/test/workspace/build.gradle
sourceCompatibility = 1.6
version = 1.0

allprojects {
    apply plugin: 'idea'
}

subprojects {
    apply plugin: 'java'
    repositories {
        mavenCentral()
    }

    dependencies {
        compile(
            'com.google.guava:guava:13.0.1',
            'log4j:log4j:1.2.17',
            // fileTree(dir: "${rootProject.projectDir}/lib", include: '*.jar')
        )
        testCompile(
            'junit:junit:4.10',
            'org.mockito:mockito-all:1.9.0',
        )
    }
}

project(':Server') {
    jar {
        from { configurations.compile.collect { it.isDirectory() ? it : zipTree(
it) } }
        manifest { attributes 'Main-Class': 'main.java.StartServer' }
    }
    dependencies {
        compile(
            project(':ServerUtil'),
            files(
                '../Lib/jdom.jar',
            )

        )
    }
}

def jarProjects() {
    subprojects.findAll { project -> project.name != 'ServerUtil'}
}

task deploy(description: 'Copies the artifacts') {
    ext {
        distDir = file("dist")
    }
    doLast {
     jarProjects().each { project ->
            def jarDist = project.file("${distDir}/${project.name}")
            def confDist = project.file("${distDir}/${project.name}/config")
            def confDir = project.file("config")
            def jarDir = project.file("${project.buildDir}/libs")
            copy {
                from jarDir
                into jarDist
                include "*.jar"
            }
            copy{
                from confDir
                into confDist
            }
        }
    }
}
</pre>

* Post-build Actions

<pre>
/bin/bash start.sh
</pre>

<pre>
# //var/lib/jenkins/jobs/test/workspace/start.sh
kill -9 `lsof -t -i :8081`
nohup java -jar Server.jar &
</pre>


