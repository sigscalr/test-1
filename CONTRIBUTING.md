# Hyperion Contributing Guide

* [New Contributor Guide](#contributing-guide)
  * [Ways to Contribute](#ways-to-contribute)
  * [Find an Issue](#find-an-issue)
  * [Ask for Help](#ask-for-help)
  * [Pull Request Lifecycle](#pull-request-lifecycle)
  * [Development Environment Setup](#development-environment-setup)
  * [Pull Request Checklist](#pull-request-checklist)

Hello there! We are glad that you want to contribute to our project! 💖

As you get started, you are in the best position to give us feedback on areas of
our project that we need help with including:

* Problems found during setting up a new developer environment
* Gaps in our Quickstart Guide or documentation
* Bugs in our automation scripts

If anything doesn't make sense, or doesn't work when you run it, please open a
bug report and let us know!

## Ways to Contribute


We welcome many different types of contributions including:

* New features
* Builds, CI/CD
* Bug fixes
* Documentation
* Issue Triage

Not everything happens through a GitHub pull request. Please go to our [contact us](https://www.sigscalr.io/contact.html) and let's discuss how we can work together. 


## Find an Issue

We have good first issues for new contributors and help wanted issues suitable
for any contributor. [good first issue](https://github.com/sigscalr/hyperion/labels/good%20first%20issue)** has extra information to help you make your first contribution. 
[help wanted](https://github.com/sigscalr/hyperion/labels/help%20wanted)** are issues suitable for someone who isn't a core maintainer and is good to move onto after your first pull request.

Sometimes there won’t be any issues with these labels. That’s ok! There is
likely still something for you to work on. If you want to contribute but you
don’t know where to start or can't find a suitable issue, you can 
[contact us](https://www.sigscalr.io/contact.html)**

Once you see an issue that you'd like to work on, please post a comment saying
that you want to work on it. Something like "I want to work on this" is fine.

## Ask for Help


The best way to reach us with a question when contributing is to ask on:

* The original github issue
* Our Slack channel : Hyperion public channel**

## Pull Request Lifecycle

1. Open a PR and request reviews only after the full PR is ready for review.
   - Open *DRAFT* PRs to get feedback on incomplete PRs and let reviewers know what they should be reviewing
2. Before merging, make sure that all CI/CD tests pass
   - For larger PRs touching multiple modules, run tests locally using `sigscalr-client`
   - In addition, for larger PRs, make sure to validate ES compatibility
   - If any configurations were added or changed, add them to `GETTING_STARTED.md`
3. Always **squash and merge** any branch merging to `develop`
4. Always **commit merge** when merging `develop` to `main`
5. Merged pull request changes will be deployed with the next release.


## Development Environment Setup
Download golang version that is defined in `go.mod` and make sure git is installed.

VS Code is the recomended IDE and offers good extensions and tools that will help developers write code.

To locally run `golinter`, install from https://golangci-lint.run/usage/install/#local-installation

### Start up Hyperion

Once golang is installed, start up Hyperion by running the following command at the root of the repo:
```
go run cmd/sigscalr/main.go --config server.yaml
```

By default, the UI server will start up on port `80` and the backend will start on port `8081`.

You should be able to access `http://localhost:80` and see the Hyperion UI. If you are not able to, check `sigscalr.log` for any error messages.


### Send Data to Hyperion

To send data, clone the [sigscalr-client](https://github.com/sigscalr/sigscalr-client) repo.

In another terminal, start the ingestion via `sigscalr-client` by running:
```
go run main.go ingest esbulk -t 10_000 -d http://localhost:8081/elastic --processCount 1 -n 1 -b 500 -g dynamic-user
```

Send metrics via:
```
go run main.go ingest metrics -d http://localhost:8081/otsdb -t 1_000_000  -m 5 -p 20 -b 10_000
```

Look through the [sigscalr-client ReadMe](https://github.com/sigscalr/sigscalr-client/README.md) to see all command arguments.


### Send Queries on Hyperion

Using the UI, you should be able to send queries using our pipe search query langauge. Look through the dropdown highlighting different query syntax and try running some test queries on the UI.

The sigscalr-client also supports sending queries using:
```
go run main.go query -d http://localhost:80/elastic -n 10 -v
```


The sigscalr-client also supports sending queries using:
```
go run main.go query esbulk -d http://localhost:80/elastic -n 10 -v
go run main.go query otsdb -d http://localhost:80/elastic -n 10 -v
```


## Pull Request Checklist

When you submit your pull request, or you push new commits to it, our automated
systems will run some checks on your new code. We require that your pull request
passes these checks, but we also have more criteria than just that before we can
accept and merge it. We recommend that you check the following things locally
before you submit your code:

lint:
	golangci-lint run --timeout=3m

ut:
	$(GO) test ./... -count 1

build:
	$(GO) mod download
	$(GO) build -o sigscalr cmd/sigscalr/main.go

run:
	$(GO) build -o sigscalr cmd/sigscalr/main.go
	./sigscalr --config server.yaml

