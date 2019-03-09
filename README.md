# pycodeq
How to do code analysis with sonarqube for python projects

*local*
For development, you could ouser a local sonarqube server (running in a container).
Wit this configuration, once you think you are ready to commit, you can verify your code against pylint and do some code coverage. You can always do this using separate tools (pylint, pytest-cov, coverage, etc.) _But_ having all the results in one single web interface, and even being able to track evolution helps too.

*remote*
If your organization has specified certains thresholds for coverage, or deactivated some rules, you will be able to conform to them by analyzing first locally, and avoiding code rejections in a PR.

Here is a list of steps for each scenario:

## local

+ Get a copy of the sonarqube server docker image
+ run it
+ activate the pylint rules in a new quality profile
+ configure your project
+ install sonar-scanner
+ run sonar-scanner


## cloud

+ Activate the sonarcloud in github
+ configure your repository
+ add the pylint rules


## Activate pylint rules

The default sonarqube server (from docker and sonarcloud.io) does not include the pylint rules.
[see here for the issue](https://community.sonarsource.com/t/pylint-and-qualityprofile/5462/9)
To activate them, create a new quality profile for python. 
Make it inherit from Sonar way, then activate the pylint repository and bulk add those rules.

After that, add the newly created profile to your project or make it the default for your python projects.


## Running the analysis

After installing sonar-scanner, either create a `sonar-project.properties` or run the scanner with options to specify the pylint executable or report, the coverage report and also bandit security report.
