# GitHub Pull Request Coverage Status Plugin for Jenkins

[![Build Status](https://travis-ci.org/jenkinsci/github-pr-coverage-status-plugin.svg?branch=master)](https://travis-ci.org/jenkinsci/github-pr-coverage-status-plugin)
[![Coverage Status](https://coveralls.io/repos/github/terma/github-pr-coverage-status/badge.svg?branch=master)](https://coveralls.io/github/terma/github-pr-coverage-status?branch=master)

https://wiki.jenkins-ci.org/display/JENKINS/GitHub+PR+Coverage+Status+Plugin

Parse code coverage report generated by build and post code coverage status comment to GitHub pull request:
![Example](https://raw.githubusercontent.com/jenkinsci/github-pr-coverage-status-plugin/master/screenshot.png)

## Supports coverage reports
* Jacoco ```jacoco.xml```
* Cobertura ```cobertura.xml``` or ```cobertura-coverage.xml```
* Clover ```clover.xml```
 
## How to use
* Select or create new Jenkins build
* Ensure that build create code coverage report file
* Configure build to be triggered by [GitHub pull request builder plugin](https://wiki.jenkins-ci.org/display/JENKINS/GitHub+pull+request+builder+plugin)
* Install plugin from Jenkins Plugin Repository
* Or manually 
 * Goto [releases](https://github.com/jenkinsci/github-pr-coverage-status-plugin/releases)
 * Download latest version of plugin *.hpi* file
 * Install to your Jenkins [guide](https://wiki.jenkins-ci.org/display/JENKINS/Plugins)
* Configure global settings of plugin
 * GitHub API URL keep blank for GitHub.com and fill if for dedicated instance of GitHub, example: ```http(s)://hostname/api/v3/```
 * Set [Personal Access Token](https://github.com/blog/1509-personal-api-tokens) (or keep blank if anonymous access enabled)
* [Optional] Add *Record Master Coverage* post build step to build which test your master
* Add *Publish coverage to GitHub* post build step to build. It should be triggered by [GitHub pull request builder plugin](https://wiki.jenkins-ci.org/display/JENKINS/GitHub+pull+request+builder+plugin)

## Troubleshooting

### No coverage picture on GitHub Pull Request Page

If you see next picture in on your pull request in GitHub:

![No coverage picture](https://raw.githubusercontent.com/jenkinsci/github-pr-coverage-status-plugin/master/no-coverage-picture.png)

In most cases that mean that your Jenkins runs on ```http``` instead of ```https```
Plugin uses same protocol as your Jenkins, however GitHub in most cases accessible by ```https```
Default browser policy to block non secure resources on secure pages from unknown domain.

To fix that you have a few options:

* Configure plugin to publish link on picture over ```https```
  * Open Jenkins
  * Click ```Manage Jenkins```
  * Click ```Configure System```
    * Find section ```Coverage status for GitHub Pull Requests```
    * Find property ```Jenkins URL for icon in Pull Request```
    * Put URL to your Jenkins with ```https``` like ```https://jenkins.my.com```
    * Save
  * Restart Jenkins
* Run your Jenkins on ```https``` by default

![Plugin settings](https://raw.githubusercontent.com/jenkinsci/github-pr-coverage-status-plugin/master/plugin-settings.png)

## Changelog

### 1.2.0

Add alternative text to coverage image for case when GitHub doesn't able to show image

### 1.1.1

Correct parsing Cobertura report for edge cases 

### 1.0.8

First public release to Jenkins Plugin Repo
