# STIG Operator

The stig-validator-operator is a group of controllers that runs within an RKE2 Kubernetes cluster.
It provides a means to deploy and manage a scanner to report on compliance to the RKE2 STIG.

The STIG Validator Controller checks the RKE2 clusters configuration against the criteria
defined for it in the RKE2 STIG as developed by RancherFederal along side DISA.

When the controller starts it will create a default stig-rke2 CR.

## Building

`make`

## Running

NOTE: This is future state.  The application entry point will be renamed eventually.

Current state:
`./bin/cis-operator`

Future state:
`./bin/stig-operator`

## License
Copyright (c) 2022 [Rancher Federal, Inc.](http://rancher.com)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
