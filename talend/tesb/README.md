Talend ESB POM
--------------

This is a platform pom that uses dependencyManagement imports 
of apache parent poms from the component Apache projects to establish a
consistent set of dependency versions for use by apps being built on the Talend
ESB.  

It does not have dependency management features of its own with the exception of
tweaking the spring framework to exclude commons logging.  It adds a few 
dependencyManagement entries for a few (unused) spring dependencies to ensure
consistency.  It also tweaks the spring-framework to exclude the 
commons-logging dependency. 

All of the relevant overrides of Apache products should be explicitly identified
via the Talend ESB properties and dependencyManagement imports.  In general,
there should not be a need for many Talend ESB dependencyManagement imports.

There are some problems which can arise with this approach on occasions.  For
example, Talend ESB 5.2 uses Karaf 2.2.9 but substitutes Jetty 7.6.7 for the
default Jetty 7.5.4 used in Karaf.  The resulting dependencyManagement imports
provide the Jetty 7.5.4 via the Karaf parent pom.  This may be sufficient
fidelity in development in most cases since unit testing can be done without
using Jetty using camel-maven:run.  But if the jetty-maven-plugin is used or
other details of jetty configuration are impacted then these differences could
have an impact.

It is recommended that explicit dependencyManagement for the Talend ESB be
centralized.