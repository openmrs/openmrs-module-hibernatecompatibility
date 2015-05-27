OpenMRS Hibernate Compatibility
===============================

# Overview

- The Hibernate Compatibility module provides a compatibility layer for OpenMRS modules to run under both Hibernate 3 (OpenMRS core < 1.12) and Hibernate 4 (OpenMRS core >= 1.12), by introducing custom wrapper objects to hide API incompatibilities.

- The need for this module  came about during an upgrade of the Hibernate libraries from v3.6 to v4 in OpenMRS Core 1.12, when it was discovered that (in the words of Juergen Hoeller of Spring):

> "I'm afraid there is a key difference between the Hibernate 3.6 and 4.0 APIs: SessionFactory.getCurrentSession() used to declare 
> org.hibernate.classic.Session as its return type in 3.6 but returns org.hibernate.Session in 4.0. Unfortunately, this is not very obvious.
> Any code compiled against Hibernate 3.6, or against a classpath where the Hibernate 3.6 jar sits before the Hibernate 4.0 jar,
> will be compiled against the old version of that method and will raise a NoSuchMethodError when running against Hibernate 4.0.
> Since this is about calls in your own repository classes, there is nothing we can do about this. You need to make sure that all 
> your repository implementation classes are being compiled against the same Hibernate API generation that they run against."

Juergen Hoeller

# Getting Started

- As a module developer, add a Maven dependency to hibernate-api in any necessary pom.xml files, add an aware-of dependency in the module's config.xml, update any DAOs that are using a Hibernate SessionFactory class + Spring sessionFactory bean to use DbSessionFactory class + Spring dbSessionFactory bean instead.  
An example of the changes are shown at: [ Hibernate Compatibility update example for Atlas ](https://github.com/openmrs/openmrs-module-atlas/compare/master...kristopherschmidt:ATLAS-118)

- As an OpenMRS implementor, install this module _before_ installing any modules with a hibernatecompatibility dependency (TODO: how do we know this if it's only an aware-of dependency), only when running the following versions of Core:  
-- 1.8.* or less  
-- 1.9 to 1.9.8  
-- 1.10 to 1.10.1  
-- 1.11 to 1.11.2  

- Core versions 1.12+, 1.9.9+, 1.10.2+, and 1.11.3+ already contain all of the hibernatecompatibility code and beans, so the hibernatecompatibility module should not be used when running these versions.


# For more information 

- View the initial OpenMRS topic at: [SessionFactory Issue After Hibernate 4 Upgrade](https://talk.openmrs.org/t/sessionfactory-issue-after-hibernate-4-upgrade/1864)

