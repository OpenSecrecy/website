---
title: Installation
description: Installing Encrypted-secrets Kubernetes Operator and Cryptctl CLI
categories: [Documentation]
tags: [docs]
weight: 1
---

{{% pageinfo %}}
Installing Encrypted-secrets Kubernetes Operator and Cryptctl CLI
{{% /pageinfo %}}

## Prerequisites

1. Working Kubernetes cluster
2. Kubectl configured to access the cluster


## Installation

1. Install encrypted-secret operator

```bash
export RELEASE=v0.1.0 
kubectl apply -f https://github.com/OpenSecrecy/encrypted-secrets/releases/download/$RELEASE/encrypted-secrets-controller.yaml
```
**Note:** You can find the latest release [here](https://github.com/OpenSecrecy/encrypted-secrets/releases/latest)

2. Install cryptctl CLI

```bash
brew tap opensecrecy/cryptctl
brew install cryptctl
```

**Note:** If you are not using brew, you can download the binary from [here](https://github.com/OpenSecrecy/cryptctl/releases/latest)

3. Make sure the operator is running

```bash
kubectl get pods -n encrypted-secrets-system
```

## Setup

1. Create an encryption key

```bash
cryptctl init -n <namespace> -p k8s
```

This will create a namespace scoped encryption key. `-p` flag is used to specify the encryption provider. Currently, only `Kubernetes` and `AWS_KMS` provider is supported.
In case of `AWS_KMS` provider, a KMS key will be created.

2. Create an encrypted-secret manifest

```bash
cryptctl create -f <path-to-encrypted-secret-manifest> -p <provider>
```


## Try it out!

### Prerequisites
1. Set `EDITOR` environment variable to your favorite editor. This will be used to open the encrypted-secret manifest for editing.

```bash
export EDITOR=vim
```
or
```bash
export EDITOR="code -w"
```

Once the encrypted-secret manifest is created, you can use it to add secrets and encrypt them.

**Note:** In case of `k8s` provider, make sure your kube-context is set to correct cluster.
```bash
cryptctl edit <encryptes-secrets-manifest.yaml>
```

This will open the manifest in your default editor. Add the secrets you want to encrypt in the `data` section of the manifest. Save and close the file.

