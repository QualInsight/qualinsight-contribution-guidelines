# Toolset for QualInsight projects
This repository provides a toolset and guidelines for developers contributing to QualInsight projects.

## How to contribute to a QualInsight project ?

All QualInsight projects follow a "feature branch" approach. As such, we ask you to respect the following few steps and guidelines.

1. if you plan to fix a bug / add a new feature / help on a specific topic, please first create a GitHub issue in the project and explain what you plan to do.
2. if your contribution implies consequent work, please first discuss with us the design of your contribution. This will ease the PR review and make sure that there will be no dispute concerning the design. 
3. fork the project you want to contribute to
4. configure your IDE in order to respect QualInsight coding guidelines (see below)
5. code your contribution as well as corresponding unit tests (see below)
6. analyze your code using SonarLint default configuration
7. commit your changes using wellformed messages and comments (see below)
8. once you're done, make a wellformed pull request (see below)

# What coding guidelines do I need to follow ?

* in order to avoid style issues and ease PR reviews, your IDE must be configured in order to use configuration files provided by this repository.
* if no configuration is provided for your IDE, please contact us.
* public API must be at least 90% documented using javadoc
* classes must respect the "single responsibility principle" (SRP)
* methods must be concise, i.e. method complexity should not be greater that 10
* class names and method names must be clear and informative
* new code must be tested, expected UT coverage for new code is 80%
* test method names must follow expected naming scheme (see below)
* if a test needs to assert multiple conditions that need to be considered as a whole, please use assertj's `SoftAssertions`
* if you need to add a third party library, please first discuss with us in order to make sure that we agree on the library and on the version to be used.
* if you need to change a library version, please first discuss with us in order to make sure that we won't introduce compatibility issues
* if possible do not mix quality improvement commits with functional modifications commits

# Why should I add tests and what is the UT coverage that is required ?

The reasons for asking you to run existing tests and to provide tests for your contribution are twofold:

* The code you add should not break existing code
* Future modifications should not break your contribution

In order to achieve this, we ask you to:

* make sure that existing tests still pass after having added your contribution
* that you update existing tests if they need to be adapted
* that you add tests for your contribution (at least 80% coverage)

What we do not ask you to do (but help is really appreciated):

* add missing tests for preexisting code

# How should I name my UT methods ?

We want to have our unit test methods self explanatory and as clear as possible. Therefor they must respect the following convention:

```
// when testing a SUT's constructor
<class name>_(when|with|using)_<whatever you want>_should(Not)?(Throw)?_<whatever you want>
// when testing a SUT's method
<tested method name>_(when|with|using)_<whatever you want>_should(Not)?(Return|Throw)?_<whatever you want>
// when testing a SUT's constant
constant_<tested constant name>_should(Not)?_<whatever you want>
```

While using `_` may seem ugly, this template brings two advantages:

* test methods are nicely ordered in your IDE's class overview
* when a test fails it is extremely easy to know what method has been impacted

# What is a "wellformed commit message" ?

A wellformed commit message respects this template: `<imperative verb> <concise subject> #<issue id>`.

Examples:

```
improve documentation #12
add unit tests #12
lower method complexity #12
```

Please avoid this kind of commit message:

```
I improved the documentation
#12
unit tests
#12 lower method complexity
```

# Why do I have to use SonarLint ?

Once your PR is merged, the project will be analysed by SonarQube's Nemo instance. We ask you to use SonarLint with a default and up to date configuration in order to make sure that your contribution does not introduce quality issues. We do our best in order to have our projects pass SonarQube's quality gate and ask you to do the same. If you do not want to use SonarLint and prefer to use your own SonarQube instance for detecting issues it is ok as long as:

* your code does not introduce new blocker issues
* your code does not indroduce new critical issues

# Updating licences

If you add new files, the have Maven build won't pass if you don't add missing licence headers. All QualInsight projects are configured in order to ease this task. All you have to do is to run the following command:

```
mvn license:format
```

# Pull requests

Pull requests should be named after the name of the issue they are fixing. For instance if the issue you're fixing is named "add image caching capabilities" and has the id `12`, the pull request should be named `add image capabilities #12`. In other words the name of the pull request should be:

```
<issue name> #<issue ID>
```
