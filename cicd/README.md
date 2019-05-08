# CD/CD Practices  

| Practice | Description  |  Enabling Tools or Platforms |  
| -------- | ------------ |  --------------------------- |  
| Version Control | Everything required to build application should be in version contol such as github or bitbucket (git) to store all software assets: source infrastructure-as-a-code automation code, test scripts configuration files, install scripts and so on. Branching Strategy Trunk-based development with optional short-lived branches that eliminate need for hardening sprints/phases. |  Github, Bitbucket, Mercurial | 
| Code Coverage | Implement automated unit testing and percentage of application code coverage by unit tests is measured and monitored. 80% or above unit tests must pass. All unit tests must be executed locally before code commit. Quality gates should be configured to break the build if test coverage thresho Code coverage level must increase as coverage improves.  | SonarQube, JaCoCo. OpenClover, Istanbul, Coverage.py, JUnit (*Unit), TestNG, Jest | 
| Static Analysis | A static code analysis is performed on every build and Critical / Blocker items should cause build breakage. Use checkstyle, code quality checkers. | FindBugs. SonarQube, Google Java Check Style, Google or AirBnB JavaScript check style |  
| Security Analysis | A security scan is performed with every build cycle or nightly. Critical / High items should cause build breakage. Create stories to address security items in every sprint. | Fortify security scan |  
| Open Source Scanning | An open source legal and security scan is performed in every build. Use non-compliance to open source policies to break the build. Address Critial/High items in every sprint. Address open source compliance issues early in the cycle so not pick an open source software related issue late in the cycle which can impact development. |  Blackduck |  
| Artifact Management | Artifacts must be published in an artifact management repository with versioning and metadata about its origin.|  Nexus or Artifactory Repository | 
| Automated Provisioning of Infrastructure | Use automated provisioning i.e. infrastructure-as-a-code to provision infrastructure in private and on public cloud to automate infrastructure provisioning in Production & Non-Production. | PCF Bosh, AWS CloudFormation, Chef, Puppet, Terraform, Ansible |  
| Immutable Servers | Non-Prod and Production servers are never modified unless there is emergency incident. They are replaced with automated provisioning. | Docker, Kubernetes, PCF/Cloud Foundry | 
| Automated Build, Test, Deployment Pipeline | Code changes are built, deployed and tested without manual intervention. | Jenkins, Concourse, TravisCI, Gitlab, CircleCI, CodeShip. Gradle, Maven |  
| Automated Integration Testing | Every deployment has some level of test automation included which perform integration testing as part of the CI/CD pipeline. | TestNG, DBUnit, JsUnit, xUnit, Cucumber, RestAssured, Selenium | 
| Automated Performance Testing | As part of the CI/CD pipeline, prior to production deployment, performance tests are initiated and key performance metrics are captured and compared to established threshholds for the KPI. Use APM (e.g. New Relic, App Dynamics etc.) to capture performance metrics a alerts. The production deployment should be stopped performance tests fail. | JMeter, Grinder, LoadRunner, BlazeMeter, Gatling, Tsung |
| Automated Rollback | If deployment process fails, rollback of the application and configuration is automated. Use Blue/Green deployment. |    |  
| Zero-Downtime Production Releases| Achieve zero downtime through blue/green, canary or N+1 releases. |
| Feature Toggle | Use feature toggles to activate/de­activate new features in production via configuration. |  Togglz |

# Version Control
* [Github](https://github.com/)
* [Bitbucket](https://bitbucket.org/)
* [Gitlab](https://about.gitlab.com/)
* [Mercurial](https://www.mercurial-scm.org/)

## Trunk-Based Development
* [Trunk-Based Development Web Site](https://trunkbaseddevelopment.com/)
* [trunk-based development (TBD) for apps]https://hackernoon.com/trunk-based-development-tbd-for-apps-9b654b6b198c)
* [Trunk-Based Development](http://kean.github.io/post/trunk-based-development)
* [Trunk-Based Development: What It Is and Why You Need It Now](https://rollout.io/blog/trunk-based-development-what-why/)
* [http://kean.github.io/post/trunk-based-development](https://www.thoughtworks.com/insights/blog/enabling-trunk-based-development-deployment-pipelines)
* [Trunk-Based Development- A Love and Hate Story](https://medium.com/comparethemarket/trunk-based-development-a-love-hate-story-be1587a13314)
* [Trunk-Based Development as Cornerstone of Continuos Delivery](https://www.infoq.com/news/2018/04/trunk-based-development)

## Feature Toggle
* Marting Fowler on [Feature Toggle](https://www.martinfowler.com/articles/feature-toggles.html)
* [Value of Feature Falgs in CI/CD](https://rollout.io/blog/value-feature-flags-ci-cd/)
* [Hub for Feature Flags, Toggles and Controls](http://featureflags.io/)
* List of Libraries
  * [Feature Flags SDKs & Libraries](http://featureflags.io/feature-flags/)
  * Java
    * [Togglz](https://www.togglz.org/)
    * [Flip](https://github.com/tacitknowledge/flip)
    * [Unleash](https://github.com/Unleash/unleash)
  * [JavaScript Feature Flags](http://featureflags.io/javascript-feature-flags/)
* SaaS Solutions
  * [Launch Darkly](https://launchdarkly.com/)

# Build Tools & Asset Repository Management
* [Gradle](https://gradle.org/)
* [Maven](https://maven.apache.org/)
* [Nexus Repository](https://www.sonatype.com/nexus-repository-oss)
* [JFrog Artifactory](https://jfrog.com/artifactory/)
* [JFrog Bintray](https://jfrog.com/bintray/)
* Interesting Gradle Plugins
  * [Netflix Nebula Plugins](https://nebula-plugins.github.io/)
  * Automated versioning and tagging to support [Semantic Versioning](https://semver.org/)
    * [Nebula Release Plugin](https://github.com/nebula-plugins/nebula-release-plugin)
    * [Gradle Git-Version](https://github.com/palantir/gradle-git-version)

# CI/CD Tools
* [Jenkins](https://jenkins.io/)
* [Concourse](https://concourse-ci.org/)
* [TravisCI](https://travis-ci.org/)
* [CircleCI](https://circleci.com/) - great for mobile app development with dedicated Mac Machines for builds
* [CloudBees CodeShip](http://codeship.com/)
* [Gitlab](https://about.gitlab.com/product/continuous-integration/)

# Static Analysis
## Code Style, Linting
* [Google Style Guides](https://github.com/google/styleguide) - covers languages used by Google open source projects

### Java
* [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)
* [Checkstyle for Google Java Style Guide](https://github.com/checkstyle/checkstyle)

### JavaScript
* [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
* [AirBnB JavaScript Style Guide](https://github.com/airbnb/javascript)

### Swift
* [Google Swift Style Guide](https://google.github.io/swift/)
* [AirBnB Swift Style Guide](https://github.com/airbnb/swift)

### Python
* [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)

## Security Scans
* [Fortify Scans](https://www.microfocus.com/en-us/products/static-code-analysis-sast/overview)

## Open Source Security and License Compliance Scans
* [Blackduck](https://www.blackducksoftware.com/)
* [White Source](https://www.whitesourcesoftware.com/)

## Test Coverage  
* [SonarQube](https://www.sonarqube.org/)

### Java
* [SpotBugs, formerly FindBugs](https://spotbugs.github.io/)
* [JaCoCo](https://www.jacoco.org/jacoco/)
* [OpenClover](http://openclover.org/)

### JavaScript
* [Jest](https://jestjs.io/) - Primarily for unit testing JavaScript but offers test coverage analysis
* [Istanbul](https://istanbul.js.org/)

### Scala
* [SCoverage](http://scoverage.org/)

### Python
* [Covergae.py](https://coverage.readthedocs.io/en/v4.5.x/)
* [Testing and Coverage with Python](https://developer.ibm.com/recipes/tutorials/testing-and-code-coverage-with-python/)

# Testing
## Unit Testing
### Java
* [JUnit](https://junit.org/)
* [TestNG](https://testng.org/doc/)
* [HtmlUnit](http://htmlunit.sourceforge.net/)
* [DBUnit](http://dbunit.sourceforge.net/)
* [Mockito](https://site.mockito.org/)
*
### Scala
* [ScalaTest](http://www.scalatest.org/)

### JavaScript
* [Jest](https://jestjs.io/) 
* [Mocha](https://mochajs.org/)
* [Karma](https://karma-runner.github.io/3.0/index.html)
* [Jasmine](https://jasmine.github.io/)

### Python
* [Python unittesting](https://docs.python.org/3/library/unittest.html)
* [PyTest](http://pytest.org/latest/)
* [Hypothesis](https://hypothesis.readthedocs.io/en/latest/index.html)
* [mimesis](https://github.com/lk-geimfari/mimesis) - A very useful tool to generate big volumes of fake data for a variety of purposes in a variety of languages
* Hitchhiker's Guide to Python [writing tests](https://docs.python-guide.org/writing/tests/)
* [FullStack Python Unit Testing](https://www.fullstackpython.com/unit-testing.html)

### Swift
* [Ray Wenderlich Tutotrial on iOS Unit Testing](https://www.raywenderlich.com/709-ios-unit-testing-and-ui-testing-tutorial)

## Behavior Drive Development 
* [Cucumber](https://cucumber.io/)
* [Selenium](https://www.seleniumhq.org/)
* [Test Automation with Cucumber and Selenium](https://www.softwaretestinghelp.com/cucumber-bdd-tool-selenium-tutorial-30/)

### API Testing
* [RestAssured](http://rest-assured.io/)
* [SoapUI](https://www.soapui.org/)
* [Postman](https://www.getpostman.com/)
* [Wiremock](http://wiremock.org/)
* [Pact Testing](https://docs.pact.io/) - Contract Driven Development and Testing 
  * [Pact Foundation](https://github.com/pact-foundation
* [Spring Cloud Contracts](https://spring.io/projects/spring-cloud-contract) - Consumer Driven Contracts or Contract Driven Development

# Performane Testing
* [JMeter](https://jmeter.apache.org/)
* [Grinder](https://github.com/cossme/grinder)
* [Gatling](https://gatling.io/)

# Infrastructure Automation
## Continuous Delivery (CD)
* Martin Fowler's talk on [Continuous Delivery](https://www.youtube.com/watch?v=aoMfbgF2D_4)
* [Continuous Delivery: : Reliable Software Releases through Build, Test, and Deployment Automation](https://www.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912) by Jez Humble & David Farley
## Infrastructure-as-Code & Deployment Automation
* [Ansible](https://www.ansible.com/)
* [Terraform](https://www.terraform.io/)
* [Bosh](https://www.bosh.io/docs/)
* [Chef](https://www.chef.io/)
* [Puppet](https://puppet.com/)
* [SaltStack](https://www.saltstack.com/)
* [AWS CloudFormation](https://aws.amazon.com/cloudformation/)
* [AWS OpsWorks](https://aws.amazon.com/opsworks/)
* [Google Cloud Deployment Manager](https://cloud.google.com/deployment-manager/)
* [Google Athnos](https://cloud.google.com/anthos/docs/concepts/anthos-overview)
* [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/)
* [Azure Deployment Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/deployment-manager-overview)

## Immutable Infrastructure
```Immutable infrastructure is a paradigm in which servers are never modified after they're deployed. If something needs to be updated, fixed, or modified in any way, new servers built from a common image with the appropriate changes are provisioned to replace the old ones. After they're validated, they're put into use and the old ones are decommissioned.```

* Hashicorp on [Mutable and Immutable Infrastructure](https://www.hashicorp.com/resources/what-is-mutable-vs-immutable-infrastructure)
* [An Introduction to Immutable Infrastructure](https://www.oreilly.com/ideas/an-introduction-to-immutable-infrastructure)
* [CodeShip Blog on Immutable Infrastructure](https://blog.codeship.com/immutable-infrastructure/)
* Pivotal Cloud Foundary's support for [Immutable Infrastructure for Windows](https://content.pivotal.io/blog/immutable-infrastructure-windows-and-bosh)

## Building Blocks for Immutable Infrastructure
* Kubernetes
* Docker
* Platform-as-a-Service (PaaS)
* Software Defined Networks (SDN)
