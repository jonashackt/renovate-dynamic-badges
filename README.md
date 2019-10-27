# renovate-dynmamic-badges
Example project showing how to use badge services like shields.io to create dynamic version badges for renovate managed GitHub repositories

If you don't know [renovate](https://renovatebot.com/) already, take your time to have a look. You'll love it, escpecially if you're an OpenSource maintainer - or simply have lot's of GitHub repositories :)

If you also like those shiny cool version badges like me, you'll soon find yourself in the situation, where renovate keeps your dependecies up to date - but not your version badges :( A somehow standard badge of a project like xxx could look like this:

[![versionspringboot](https://img.shields.io/badge/springboot-2.1.7_RELEASE-brightgreen.svg)](https://github.com/spring-projects/spring-boot)

Wouldn't it be great to have this badge dynamically updated simply based on the project's Maven `pom.xml`? There is a great generator for dynamic badges on [https://shields.io/](https://shields.io/). Right out of the box, your `XPATH` queries (created with a service like [http://xpather.com/](http://xpather.com/) for example) to the version of your Maven dependencies woun't work! Why? Because Maven pom.xmls use XML namespaces! Therefore I created this issue https://github.com/badges/shields/issues/4250 and got help from a shields.io maintainer. Here's it in a nutshell:


### 1. Create an XPATH query to your pom.xml

Use the *every* node and create the full path to your version:

```
/*[local-name()='project']/*[local-name()='properties']/*[local-name()='spring.boot.version']
```


### 2. Encode query for URL usage

Like with https://www.urlencoder.org/:

```
%2F%2A%5Blocal-name%28%29%3D%27project%27%5D%2F%2A%5Blocal-name%28%29%3D%27properties%27%5D%2F%2A%5Blocal-name%28%29%3D%27spring.boot.version%27%5D
``` 


### 4. Build full shields.io URL

https://img.shields.io/badge/dynamic/xml?color=brightgreen&url=https://raw.githubusercontent.com/codecentric/cxf-spring-boot-starter/master/cxf-spring-boot-starter/pom.xml&query=%2F%2A%5Blocal-name%28%29%3D%27project%27%5D%2F%2A%5Blocal-name%28%29%3D%27properties%27%5D%2F%2A%5Blocal-name%28%29%3D%27spring.boot.version%27%5D&label=springboot


### 5. Integrate in your README markdown .md file:

[![versionspringboot](https://img.shields.io/badge/dynamic/xml?color=brightgreen&url=https://raw.githubusercontent.com/codecentric/cxf-spring-boot-starter/master/cxf-spring-boot-starter/pom.xml&query=%2F%2A%5Blocal-name%28%29%3D%27project%27%5D%2F%2A%5Blocal-name%28%29%3D%27properties%27%5D%2F%2A%5Blocal-name%28%29%3D%27spring.boot.version%27%5D&label=springboot)](https://github.com/spring-projects/spring-boot)
