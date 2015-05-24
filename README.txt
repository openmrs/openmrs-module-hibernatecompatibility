Provides a compatibility layer for OpenMRS modules to run under Hibernate 3 or 4

The need for this module initially came about during development of OpenMRS core 1.12 in May 2015, when the decision was made 
to upgrade Hibernate from version 3 to version 4. However, it was discovered that (in the words of Juergen Hoeller of Spring):

"I'm afraid there is a key difference between the Hibernate 3.6 and 4.0 APIs: SessionFactory.getCurrentSession() used to declare 
org.hibernate.classic.Session as its return type in 3.6 but returns org.hibernate.Session in 4.0. Unfortunately, this is not very obvious.
Any code compiled against Hibernate 3.6, or against a classpath where the Hibernate 3.6 jar sits before the Hibernate 4.0 jar,
will be compiled against the old version of that method and will raise a NoSuchMethodError when running against Hibernate 4.0.
Since this is about calls in your own repository classes, there is nothing we can do about this. You need to make sure that all 
your repository implementation classes are being compiled against the same Hibernate API generation that they run against."

In order to fix this, it was decided that OpenMRS would implement a wrapper for SessionFactory and Session, and that all modules
would be updated to use this wrapper. The wrapper classes were added to core 1.12 and backported to core 1.9, 10, 11, and 12,
but also made available via this module for anyone that could not upgrade their version of core. This module is only required
when running versions of modules that have been updated to use DBSessionFactory, and when running the following versions of core:

1.8.* or less
1.9 - 1.9.8
1.10 - 1.10.1
1.11 - 1.11.2

This topic is further discussed at: https://talk.openmrs.org/t/sessionfactory-issue-after-hibernate-4-upgrade/1864
