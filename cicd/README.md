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
* [Gradle](https://gradle.org/)https://jfrog.com/bintray/
* [Maven](https://maven.apache.org/)
* [Nexus Repository](https://www.sonatype.com/nexus-repository-oss)
* [JFrog Artifactory](https://jfrog.com/artifactory/)
* [JFrog Bintray](https://jfrog.com/bintray/)

# CI/CD Tools
* [Jenkins](https://jenkins.io/)
* [Concourse](https://concourse-ci.org/)
* [TravisCI](https://travis-ci.org/)
* [CircleCI](https://circleci.com/) - great for mobile app development with dedicated Mac Machines for builds
* [CloudBees CodeShip](http://codeship.com/)
* [Gitlab](https://about.gitlab.com/product/continuous-integration/)

# Static Analysis
## Code Style, Linting
## Security Scans
## Open Source License Compliance Scans
# Test Coverage  
## Java
## JavaScript
## Scala
## Python
# Performane Testing

# Infrastructure Automation
## Continuous Delivery (CD)
* Martin Fowler's talk on [Continuous Delivery](https://www.youtube.com/watch?v=aoMfbgF2D_4)
* [Continuous Delivery: : Reliable Software Releases through Build, Test, and Deployment Automation](https://www.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912) by Jez Humble & David Farley
## Infrastructure-as-Code 
* [Ansible](https://www.ansible.com/)
* [Terraform](https://www.terraform.io/)
* [Bosh](https://www.bosh.io/docs/)
* [Chef](https://www.chef.io/)
* [Puppet](https://puppet.com/)
* [AWS CloudFormation](https://aws.amazon.com/cloudformation/)
* [Google Cloud Deployment Manager](https://cloud.google.com/deployment-manager/)
* [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/)
* [Azure Deployment Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/deployment-manager-overview)

