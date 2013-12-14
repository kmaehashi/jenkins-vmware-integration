Jenkins & VMware Fusion Integration
=========================================

Overview
------------------------

This shell script integrates VMware Fusion with Jenkins CI.

Features
------------------------

* On-Demand Virtual Machine Power Control
  * VMs automatically start upon request from Jenkins job, and shutdown once the job gets done.
    This saves your memory space as you don't have to keep running VMs for Jenkins slaves.

* Automatic Configuration of Jenkins Slaves
  * After starting the VM, the script automatically download the latest Jenkins slave JAR file from the master server and runs it.

* Automatic Roll-Back (optional)
  * After shutting down the VM, the script automatically rolls back the VM to the specified snapshot state.
    This assures that jobs always run in consistent environment.

Requirements
------------------------

* Host
  * OS X
  * VMware Fusion
  * Jenkins

* Guest
  * No operating system limitaions, as long as:
    * Consistent IP address (which must be accessible with the Host in both direction) must be assigned.
    * SSH server must be running and can be logged in using `ssh` command without password.
    * JRE must be installed.

Tested Environments
------------------------

* Host
  * OS X 10.9
  * VMware Fusion 6
  * Jenkins 1.538

* Guest
  * OS X 10.8 and 10.7

Configuration
------------------------

First of all, tweak the `JENKINS_URL_BASE` parameter in the script to point the Jenkins master server.

In the Jenkins Node settings, add a new Dumb Slave and configure as follows:

* Launch method: Launch slave via execution of command on the Master
* Launch command: Path to the script, with the following 4 arguments
  * IP address of the VM
  * SSH user name of the VM
  * Path to the VMware Fusion VMX file
    * Note: you need to specify \*.vmx file inside \*.vmwarevm document package.
  * Snapshot name (blank if you don't want to automatically roll-back the VM)

