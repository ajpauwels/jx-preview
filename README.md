# jx-preview

[![Documentation](https://godoc.org/github.com/jenkins-x/jx-preview?status.svg)](https://pkg.go.dev/mod/github.com/jenkins-x/jx-preview)
[![Go Report Card](https://goreportcard.com/badge/github.com/jenkins-x/jx-preview)](https://goreportcard.com/report/github.com/jenkins-x/jx-preview)
[![Releases](https://img.shields.io/github/release-pre/jenkins-x/jx-preview.svg)](https://github.com/jenkins-x/jx-preview/releases)
[![Apache](https://img.shields.io/badge/license-Apache-blue.svg)](https://github.com/jenkins-x/jx-preview/blob/master/LICENSE)
[![Slack Status](https://img.shields.io/badge/slack-join_chat-white.svg?logo=slack&style=social)](https://slack.k8s.io/)


`jx-preview` is a small command line tool for creating Preview Environments in [Jenkins X](https://jenkins-x.io/) environments.

## Overview

The [jx preview create](https://github.com/jenkins-x/jx-preview/blob/master/docs/cmd/jx-preview_create.md) command will create a new Preview environment, by default in its own unique namespace called `jx-$owner-$repo-pr-$number` using a [helmfile](https://github.com/roboll/helmfile) located by default in the `preview/helmfile.yaml` directory.

New projects created with [Jenkins X 3.x](https://jenkins-x.io/docs/v3/) already have the `preview/helmfile.yaml` included. If your repository does not include this file it will be added into git in the Pull Request as an extra commit.
 
## How it works

Creating a new preview environment creates a [Preview](https://github.com/jenkins-x/jx-preview/blob/master/docs/crds/github-com-jenkins-x-jx-preview-pkg-apis-preview-v1alpha1.md#Preview) custom resource for each Pull Request on each repository so that we can track the resources and cleanly remove them when you run [jx preview destroy](https://github.com/jenkins-x/jx-preview/blob/master/docs/cmd/jx-preview_destroy.md) pr [jx preview gc](https://github.com/jenkins-x/jx-preview/blob/master/docs/cmd/jx-preview_gc.md)

For reference see the [Preview.Spec](https://github.com/jenkins-x/jx-preview/blob/master/docs/crds/github-com-jenkins-x-jx-preview-pkg-apis-preview-v1alpha1.md#PreviewSpec) documentation


## Installation

If you are using [Jenkins X 3.x](https://jenkins-x.io/docs/v3/) then its already included by default so there's nothing to install.

If you are not using [Jenkins X 3.x](https://jenkins-x.io/docs/v3/) then you need to install the `jx3/jx-preview` chart to:

* install the [Preview](https://github.com/jenkins-x/jx-preview/blob/master/docs/crds/github-com-jenkins-x-jx-preview-pkg-apis-preview-v1alpha1.md#Preview) custom resource used to track the Preview environments
* setups a `CronJob`  to garbage collect `Preview` environments when the Pull Requests have been closed or merged 



To install the `jx3/jx-preview` chart using [helm 3.x](https://helm.sh/) try the following::


- Add jx3 helm charts repo

```bash
helm repo add jx3 https://storage.googleapis.com/jenkinsxio/charts

helm repo update
```

- Install (or upgrade)

```bash
# This will install jx-preview in the jx namespace (with a jx-preview release name)

helm upgrade --install jx-preview --namespace jx jx3/jx-preview
```

## Uninstalling

To uninstall the chart, simply delete the release.

```bash
# This will uninstall jx-preview in the jx-preview namespace (assuming a jx-preview release name)

# Helm v3
helm uninstall jx-preview --namespace jx
```



## Commands

See the [jx-preview command reference](https://github.com/jenkins-x/jx-preview/blob/master/docs/cmd/jx-preview.md)

