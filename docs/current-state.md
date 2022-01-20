## RancherFederal Project: STIG operator notes

The current CIS Operator utilizes kube-bench to scan a cluster for compliance to the CIS Benchmarks.  

### Disclaimer

This information is a work in progress.  As such, it might contain some data that is 'wrong' and will 
need updating.  Please check back for frequent updates.

### kube-bench

kube-bench CLI runs CIS Benchmark checks that are defined in ‘controls’ files that are represented in YAML.  
controls is composed of a hierarchy of groups, sub-groups and checks. 

Each of the controls components have an id and a text description which are displayed in the kube-bench output. 
type specifies what kubernetes node type a controls is for. Possible values for type are master and node.

### Sonobuoy

Sonobuoy is a diagnostic tool that makes it easier to understand the state of a k8s cluster by running a set of plugins.

The following 2 scrips run the sonobuoy command against the kube-bench generated results:
* [run.sh](https://github.com/rancherfederal/security-scan/blob/master/package/run.sh)
* [run_sonohuoy_plugin.sh](https://github.com/rancherfederal/security-scan/blob/master/package/run_sonobuoy_plugin.sh)

### Architecture

Current cis-benchmark operator architecture:

Existing repos:
* [aquasecurity/kube-bench](https://github.com/aquasecurity/kube-bench)
* [rancher/cis-operator](https://github.com/rancher/cis-operator)
* [rancher/security-scan](https://github.com/rancher/security-scan)
* [vmware-tanzu/sonobuoy](https://github.com/vmware-tanzu/sonobuoy)
* [vmware-tanzu/sonobuoy-plugins](https://github.com/vmware-tanzu/sonobuoy-plugins/blob/main/cis-benchmarks/README.md)

Images used:
```yaml
  ...
    repository: rancher/cis-operator
    tag: v1.0.6
  securityScan:
    repository: rancher/security-scan
    tag: v0.2.4
  sonobuoy:
    repository: rancher/mirrored-sonobuoy-sonobuoy
    tag: v0.53.2
```

mirrored - the image is hosted in the rancher docker namespace

Custom Resource Definitions (CRD) in current CIS Operator:
* ClusterScan
* ClusterScanProfile
* ClusterScanBenchmark

The configs used by kube-bench that are specific to Rancher are in the rancher/security-scan repo, under package/cfg/

I assume this is the location to create specific ‘STIG’ configs that can then be used by kube-bench?
- Yes, this is correct


### Existing Documentation
https://github.com/rancher/charts/blob/dev-v2.6/charts/rancher-cis-benchmark/2.0.2/app-readme.md
https://github.com/aquasecurity/kube-bench/blob/main/docs/controls.md


Misc Sites with good info:
* https://dischord.org/2020/10/22/rancher-cis-operator-on-any-kubernetes-cluster/
* https://sonobuoy.io/cis-benchmark-plugin/


Possible Output formats:
* json
* csv
* pdf



### TODO:
* Create architecture diagram for current design for what the cis-operator is doing
* Document the current process and how the Operator ‘operates’
* Look at ways to simplify ingestion of STIG rules/checks
