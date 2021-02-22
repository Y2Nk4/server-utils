### Install etcd (Centos 7)

```
yum install etcd -y
```

### Set-up Authorization

```shell
# Specify endpoints
etcdctl --endpoints=http://127.0.0.1:2379
# Specify users
etcdctl --user root:password
# Specify to use ETCD3 Api
export ETCDCTL_API=3
# Enable Auth
# !!!IMPORTANT!!!
# Make sure you have alread set-up a ROOT user and password
etcdctl auth enable

##################
# With Sequences
##################

# Add `root`
etcdctl user add root

# Grant root
etcdctl --user root user grant-role root root

# Create normal users
etcdctl user add ${user_name}

# Add new role
etcdctl role add ${role_name}

# Grant permission to role
etcdctl role grant-permission --prefix=true ${role_name} readwrite{|read|write} /${path_name}

# Bind user to a specific role
etcdctl user grant-role ${user_name} ${group_name}

# Enable Auth
etcdctl auth enable
```
