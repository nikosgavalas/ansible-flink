
# Standalone Apache Flink cluster deployment with Ansible

## Usage

### Hosts

Edit the [hosts.ini](hosts.ini) file by adding the hostnames or IPs of the cluster's machines under the group `flink`. 

Use the `flink_type` variable to specify which node will be `master` (JobManager) and set the others to `slave` (TaskManager).

If you want you can set all the nodes to `slaves`, and execute the JobManager locally to your PC.

### Configuration Variables

Next, go ahead and edit the default values in the [flink](group_vars/flink) file, and the `remote_user` for your machines in the [all](group_vars/all) file.

### Run

Run the playbook with:

```
ansible-playbook -i hosts site.yml
```

### UI

Visit the `master` host at the port 8081 to access the Flink's web UI.

## Important Notes

### High Availability

This setup is **not** highly available, meaning that if the JobManager goes down, the TaskManagers will continue the execution but no new tasks can be assigned and no monitoring is possible. 

Normally, a highly available setup contains a quorum of JobManagers, which requires Zookeeper.

There are plans to support highly availability in the near future.

### System Services

Flink runs as a service with `systemd`, and by default it is `enabled` on system startup. Edit the corresponding variables to avoid such behavior. 
