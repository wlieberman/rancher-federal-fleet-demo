# rancher-federal-fleet-demo

## A demo of Fleet managing apps in multiple clusters via Rancher
For experienced users, please scroll to the bottom for the TL;DR instructions. The instructions below are intended for newer users starting out with Fleet.

## Getting started
Pre-requisites:
- A working Rancher 2.5.6+ cluster
- A forked version of this repository

Instructions:
- Edit the `ingress-ip-domain` under `Settings` in the Cluster Manager UI
  - Change from `xip.io` to `nip.io`
- Deploy two or more clusters (provider agnostic)
- Navigate to `Cluster Explorer` -> `Continuous Delivery`
  - Under `Continuous Delivery` click `Cluster Groups` (sidebar)
    - Click `Create`
    - Populate the form with the following:
      - Name: fleet-demo
      - Cluster Selectors
        - Key: fleet-demo
        - Operator: Exists
      - Click `Create` (bottom right)
  - Under `Continuous Delivery` -> `Git Repos`, click `Create`
    - Populate the form with the following:
      - Name: rfed-demo
      - Repository URL: [https://github.com/myUsername/thisForkedRepository.git (selflink)](./)
      - Watch - A Branch: main **important: github's default is now main
      - Deploy To: Target Type: fleet-demo (Under Cluster Groups at the very bottom of the drop-down)
    - Click Create
- Navigate back to `Cluster Manager`
  - Select your first cluster, then click the 3 dot menu and choose `Edit`
    - Expand the box titled `Labels & Annotations`
      - Click `Add Label`
      - Populate the label with the following:
        - `fleet-demo` `cluster1`
    - Click `Save`
  - Repeat these steps on the second cluster
    - Select cluster, 3 dot menu, `Edit`
        - Expand the box titled `Labels & Annotations`
        - Click `Add Label`
        - Populate the label with the following:
          - `fleet-demo` `cluster2`
    - Click `Save`
- Choose a cluster and navigate back to `Cluster Explorer`
  - Choose `Ingresses` from the left sidebar
    - Find the hostname from your ingress and click on it
- In the top right drop-down, choose your second cluster
  - Choose `Ingresses` from the left sidebar
    - Find the hostname from your ingress and click on it
- Now view the app running in both tabs!

To show multi-cluster rolling update:
- Navigate back to [This git repo](./)
  - Update the `COW_COLOR` variable in fleet.yaml
  - Commit/Save your changes
- Now watch the app change before your eyes!


This works with any number of clusters.

Please try it out and give feedback!


##TL;DR Instructions (for experienced Rancher admins)
- Fork this repo
- Create n number of clusters via Rancher (or import into Rancher)
- Update ingress wildcard to nip.io
- Create a cluster group
- Create a git repo containing [this forked repository](./)
- Target it to your cluster group
- Watch the magic happen
- Make changes in this repo and watch the rolling deployments

