---
title: Examples
weight: 3
---

### **Create an encryption key**

```bash 
cryptctl init -n <namespace> -p k8s
```
![cryptctl init](img/cryptctl-init.png)

### **Create an encrypted-secret manifest**

```bash
cryptctl create -f demo.yaml -p k8s
```
![cryptctl create](img/cryptctl-create.png)

### **Edit encrypted-secrets manifest to add secret**
    
```bash
cryptctl edit demo.yaml
```
![cryptctl edit](img/cryptctl-edit.gif)