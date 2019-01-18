# Solution

Jenkins can automatically bootstrap the Go runtime with the help pf the [Go plugin](https://wiki.jenkins.io/display/JENKINS/Go+Plugin). It automatically installs a pre-defined version of Go and exports the `GOROOT` environment variable. At the moment only [scripted pipelines](https://jenkins.io/doc/book/pipeline/syntax/#scripted-pipeline) are supported. For more information see [JENKINS-55630](https://issues.jenkins-ci.org/browse/JENKINS-55630).

The pipeline is comprised of multiple build steps:

1. Compile packages and dependencies.
2. Run unit tests and publish code coverage result to Codecov.
3. Run code quality analysis using `golangci-lint`.
4. Build and release the binaries to GitHub if the current commit points to Git tag.

The pipeline references environment variables, credentials and tools that need to be set up manually.

1. The Go version needs to be configured under _Manage Jenkins > Global Tool Configuration > Go_.
1. The environment variable `CODECOV_TOKEN` needs to provide the Codecov token. Environment variables can be configured under _Manage Jenkins > Configure System > Environment variables_.
2. The credential `GITHUB_TOKEN` needs to provide a valid GitHub token. Credentials can be configured under _Manage Jenkins > Configure Credentials_.