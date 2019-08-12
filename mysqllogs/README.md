# MySQL Logger

MySQL Logger Helm Chart sets up a reverse proxy 
using [ProxySQL](https://proxysql.com/). The setup is optimized
to capture query logs on a MySQL instance. 

Note that ProxySQL has a lot of features to support a complex MySQL
infrastructure. This project does not expose any features other than 
those required for a simple reverse proxy for a MySQL instance.

## Usage

### Before You Get Started

Choose a name for the helm chart.

Create two persistent volumes for data and log directories. It is important
that the persistent volumes have the label:
- app:<name>

### Installation

    helm install -n <name> mysqllogs/

### Uninstall

    helm delete mysqllogs

### Usage

    
    # Connect as proxysql admin
    kubectl exec -it $POD_NAME -c proxysql -- mysql -h 127.0.0.1 -u {{ .Values.proxysql.config.adminUser }} \
       -p {{ .Values.proxysql.config.adminPassword}} -P {{ .Values.proxysql.config.adminPort }}

    # Connect as a user. 
    mysql --default-auth=mysql_native_password -h $NODE_PORT -P $NODE_IP -h <user> -p<password>

### Administration

#### Add MySQL Hosts

mysqllogs allows you to add one MySQL server as part of the configuration. If you need more 
control, connect to ProxySQL as an admin and add more hosts. Refer to [ProxySQL docs](https://github.com/sysown/proxysql/wiki/MySQL-Server-Configuration)
    
#### Add MySQL Users

Connect to ProxySQL as an admin and add more users. Refer to [ProxySQL docs](https://github.com/sysown/proxysql/wiki/Users-configuration)

## Architecture

### Containers
The Helm Chart sets up a Kubernetes Pod with the following containers:
- ProxySQL: Runs ProxySQL as a reverse proxy.
- LogRotate: Contains a cron job that runs logrotate. LogRotate manages proxysql log files.
- LogStdout: Tails all logs in the ProxySQL log directory.

### Service (NodePort)
ProxySQL is exposed as a NodePort. 
- NodePort: Exposes ProxySQL to applications outside the Kubernetes cluster.

### Volumes

There are two volumes to expose configmaps to ProxySQL and LogRotate. 
- proxysql-configmap mounted at /etc/proxysql/proxysql.cnf
- logrotate-configmap mounted at /etc/logrotate/logrotate.conf

There are two PersistentVolumeClaims:
- DataDir: ProxySQL stores its files in this location. Mounted at /var/lib/proxysql
- LogDir: ProxySQL stores the event logs in this directory. Processed by other containers as well. Mounted at /var/log/proxysql




  
