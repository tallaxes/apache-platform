apache-platform
===============

Common pom files used to ensure consistent dependency management for Apache 
ESB projects.  Note that although provided as apache v2 licensed code, this
project is not part of an Apache Software foundation project.  The "apache
platform" just refers to the fact that the project is intended to compose
multiple apache projects together into a logical "platform" using a simple,
consistent,and repeatable approach.

### Motivation

Maven can only support one line of inheritance.  Aggregation via modules in a
pom project is different.  In an enterprise setting this constraint may be a
problem.  Projects are likely to evolve on a different cycle; having a
common parent may not be possible when two modules diverge.  This results in
more time-consuming copy-and-paste configuration of poms; and it also requires
developers to manually update versions.

Individual developers need to identify which artifact versions to use.  If the
versions happen to have been included in an example pom they are lucky - if the
example is known to kept up to date.  If a component has not been used in the
example pom, they are left to search the source code.  The latter approach is
not very friendly for beginning maven users or even modestly skilled ones who
are understandably lazy.

Even when this is done, selecting the correct version of an artifact that is
used in more than one Apache project may be difficult, e.g. if an artifact is
used in CXF and Camel, which version should be used?  Once a version is
selected, there is no means of enforcing consistency across multiple projects
created in a team environment.

Finally, even if a solution can be found in a particular case using parent poms,
the solutio is tightly coupled to the local directory structure via relative
paths.  This means either separate github projects are coupled to each other in
order to build correctly, or they have to be merged into a single project, both
of which are bad.

### Solution Approach

An alternative approach is to use the dependencyManagement feature of maven to
centralize version management.  In particular, rather than hand editing the bulk
of the dependencies, maven allows [importing dependencyManagement] from other
pom files.  Note that this is different than inheriting these settings from a
parent pom.  The imported pom is being pulled from the maven repository rather
than the local directory path.  As a result, multiple pom's can be imported, and
they leave the developer free to use maven parent pom inheritance for other
things.

### Usage

Download or clone this repository and run mvn install to ensure the necessary
pom's are loaded into the local maven repo for use by other poms.

    mvn clean install


### License

All content and accompanying materials are made available under the terms of the
Apache License v2.0 which accompanies this distribution and is available at
http://www.apache.org/licenses/LICENSE-2.0.


[importing dependencyManagement]: http://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html#Importing_Dependencies