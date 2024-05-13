# Kubernetes Goat Ansible Playbook

The goal of this playbook is to prepare a Linux host for [Kubernetes Goat](https://madhuakula.com/kubernetes-goat/), utilizing [Kubernetes in Docker](https://kind.sigs.k8s.io/) (KiND) as the Kubernetes platform. 

The playbook will clone the Kubernetes Goat git repo to the target host, as well as install all the prerequisites such as Docker, Go, KiND, Kubectl, and Helm. 
Due to the insecure nature of Kubernetes Goat, actual deployment and access of Goat is left to the user, with quick commands listed below.

# TODO

- [x] Docker Tasks
- [x] Go Tasks
- [x] Kind Tasks
- [x] Kubectl Tasks
- [x] Helm Tasks
- [x] Kuberenetes Goat Tasks

# Use

1. Copy SSH keys to target host. Ex:

   `ssh-copy-id goat@goat.home.arpa`
   
   Verify you can connect with the ssh key `ssh goat@goat.home.arpa`

2. Add the target host to an Ansible Hosts file. Ex:

   ```yaml
   [goat]
   goat.home.arpa
   ```

   This can be a hostname or IP address.

3. Run the playbook. Ex:

   `ansible-playbook -i hosts -l goat -bK kubernetes-goat.yaml`

4. Once the playbook successfully runs, deploy Goat. Ex:

   `ssh goat@goat.home.arpa 'bash /opt/kubernetes-goat/platforms/kind-setup/setup-kind-cluster-and-goat.sh'`

5. Once completed, open Goat for access. Ex:

   `ssh goat@goat.home.arpa 'bash /opt/kubernetes-goat/access-kubernetes-goat.sh'`

6. Access Goat should now be availble on the target host over HTTP on port 1234. Ex:

   `firefox http://goat.home.arpa:1234`


# Quick Commands

- **Deploy:** from deployment host `ansible-playbook -i ./hosts -l goat -bK ./playbooks/kubernetes-goat.yaml`
- **Start Goat:** on goat host `bash /opt/kubernetes-goat/platforms/kind-setup/setup-kind-cluster-and-goat.sh`
- **Access Goat:** on goat host `bash /opt/kubernetes-goat/access-kubernetes-goat.sh`
- **Teardown Goat:** on goat host `bash /opt/kubernetes-goat/platforms/kind-setup/teardown-kubernetes-goat.sh"`

# References

References used to create this playbook.

- How to Run Kubernetes Goat with Kind: https://madhuakula.com/kubernetes-goat/docs/how-to-run/kind
- ansible.builtin.file module: [https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_module.html]
- ansible.builtin.get_url module: https://docs.ansible.com/ansible/latest/collections/ansible/builtin/get_url_module.html
- ansible.builtin.git module: https://docs.ansible.com/ansible/latest/collections/ansible/builtin/git_module.html
