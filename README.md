# three-tier-app-deployment
three-tier-app-deployment
`

 































 




CONTENTS
1	REVISION HISTORY	3
2	INTRODUCTION	4
3	SCOPE OF the work	4
4	Design	4
5	Troubleshooting phase	4


















































1	REVISION HISTORY

Version	Author(s)	Comments	Date
0.1	Akash Ghosh	Initial Draft	23rd May
0.2			
 
2	INTRODUCTION

This document outlines the process for ADGM AKS podReadyPercentage Troubleshooting

3	SCOPE OF THE WORK 

The purpose of the document is to provide engineers from both ADGM and Rackspace with a set of clearly defined steps to perform ADGM AKS podReadyPercentage Troubleshooting.
4	DESIGN 

We have 9 alerts per cluster and this document outlines ADGM AKS podReadyPercentage Troubleshooting.

We will perform the troubleshooting starting with one cluster, but these steps can be generalized for other clusters as well. We are considering the cluster kube-myadgm-prd-uaen-01 for demo.

Pre- Requisite: 
•	Ensure Kubectl CLI tool is installed to interact with API server. 
•	Also ensure you have the right set of RBAC roles to access the cluster
•	Make sure ADGM VPN is connected.
•	Bash based CLI is preferred since a lot of commands are Linux Based
Step 1: Login to AKS Cluster. Click on Connect.
Connect to the cluster using the Connecting and General Troubleshooting SOP.

Troubleshooting for Alert Specific

Alert: [AKS]-KubernetesService-Performance-podReadyPercentage is less than threshold-prd

This triggers an alert when it breaches the threshold set for Percentage of pods in ready state by controller and Kubernetes namespace.

We need to identify the Pods that are not ready and then check the details of the Pod activity to identify the reason why the Pods are not running


Step 1:  Identify from the browser for the Pods not running:
Navigate to cluster > Workloads >Pods and review the Pods where it is not ready.  

You can get more details about the Pod by clicking on the Pod that is not ready and check the Overview and Events Tab
